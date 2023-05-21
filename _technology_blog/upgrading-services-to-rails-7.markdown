---
layout: post
title: Upgrading Services to Rails 7
date:  2023-05-21 16:00:00
categories: main
banner_image: "upgrading-to-rails-7.jpeg"
---

We upgraded one of our backend services from Rails version 5.2 to 7.0 a few months ago. This blog outlines the path to upgrading the services, the challenges we came across, and the learnings on the way.

### Upgrading the dependencies

Initial research revealed that the service had a dependency on an internal gem. This gem used `ActiveRecord`, `ActiveSupport`, and `ActiveModel`. Also, a few other services were using this gem.

The first step was to upgrade this gem to support versions 5.2 to 7.0. We were making it backward compatible with other services. We did an incremental upgrade. First, we added support for version 6.0, then 6.1, and finally 7.0.

Once we accomplished this, the actual work of upgrading the service to Rails 7 began.

### Upgrading the Service

We decided to do this incrementally as well. Upgrade the service from Rails version 5.2 to 6.0 to 6.1 and finally to 7.0. Testing and deploying after every upgrade.<br><br>

#### Upgrade service to Rails version 6.0

The first step in this upgrade was to update the gems and dependencies supporting Rails version 6.0. Good test coverage was an ally here. It helped us make the changes without the fear of breaking functionality.

#### Failures encountered

**Failure caused due to the change in the behavior of the *where* clause**.<br>

If the value was out of range, previous versions of rails on querying DB returned `ActiveRecord::RangeError`. This behavior changed in rails 6, to avoid running the query against out-of-range numbers and return an empty array instead.<br>

**Resolution**: Updated the tests to match the new expected result.<br>
More details on the [Rails 6 - RangeError not raised while interacting with ActiveRecord](https://github.com/rails/rails/issues/38309)

Once this change was complete, we deployed it to the staging environment, tested, and then deployed to production.<br><br>

#### Upgrade the ruby version to 2.7.0

Since Rails 6.1 requires ruby versions 2.5 and up, and Rails 7 requires ruby version 2.7 and up, we upgraded the service from 2.5 to 2.7. <br><br>

#### Upgrade service to Rails version 7.0

We encountered no issues while upgrading rails 6.0 to 6.1. The service was upgraded and deployed to production with Rails 6.1. Then, we started upgrading the service to 7.0. Here was where we encountered more failures.

#### Failures encountered

1. Unable to reload models in initializers.<br>
**Resolution:** Added `ActiveSupport::Reloader` to allow reloading the file.

2. Files under the *Concerns namespace* were not loading.<br>
Applications running in *classic mode* needed to use *Zeitwerk mode* from Rails 7 onwards. **Zeitwerk gem** usage for rails 7.x changed how the concerns are defined.<br>
**Resolution:** Concerns module wrapping was removed from file names, which fixed the issue.

3. Unable to resolve file names such as `Author_ID`<br>
`AuthorID` was being resolved to `author_i_d` instead of `author_id` because of *Zeitwerk mode*.<br>
**Resolution:** Adding inflections resolved the naming issues.<br><br>

#### Resolving Deprecation Warnings

1. `Top level::CompositeIO is deprecated, require 'multipart/post' and use Multipart::Post::CompositeReadIO instead!`<br>
The cause was usage of an older version of the Faraday gem<br>
**Resolution:** Updating faraday gem resolved this issue.

2. `Using legacy connection handling is deprecated. Please set legacy_connection_handling to false in your application`<br>
The reason for this warning was an update in connection management for rails versions greater than 6.1. <br>
**Resolution:** Marking `config.active_record.legacy_connection_handling = false` resolved this issue. <br>
Find more information on this [here](https://guides.rubyonrails.org/active_record_multiple_databases.html#migrate-to-the-new-connection-handling). <br><br>


#### Failing CI build

After fixing the all the issues we encountered a failing CI build.

`rake aborted! Don't know how to build task 'db:structure:load' (See the list of available tasks with rake --tasks). Did you mean? db:test:load` <br>

On investigating, we determined that the cause was the deprecation of `db:structure:load` in favor of `db:schema:load`. The structures and schemas are now handled by` db:schema:load`. <br>
**Resolution:** Updating commands to use `db:schema:load` resolved this issue.<br>
Find more information on this [here](https://blog.saeloun.com/2020/09/30/rails-deprecates-db-structure-commands.html).

### Conclusion

Our initial approach was upgrading the service from rails 5.2 to 7.0 directly. Needless to say that we did not go through with it. We realized that there were too many changes all at once. The dependencies needed an upgrade to support Rails 7 without breaking other services. Even with that accomplished there were too many changes in the service itself. It is a heavy-traffic service. The direct upgrade would have been dangerous. We wanted to make sure that this upgrade does not cause any outages. That's when we decided to do the upgrade incrementally. This approach ensured that everything was backward compatible, which reduced the chance of an outage. One tradeoff of this approach was, it took us longer than the direct upgrade. But for our case, the pros of safely upgrading the service outweighed the cons. 