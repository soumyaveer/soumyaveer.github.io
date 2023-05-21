---
layout: post
title: Upgrading Services to Rails 7
date:  2023-05-20 16:00:00
categories: main
banner_image: "upgrading-to-rails-7.jpeg"
---

A few months ago, we upgraded one of our backend services from rails version 5.2 to 7.0. This blog outlines the path to upgrading the service, the challenges we came across, and the learnings on the way.

### Upgrading the dependencies

Initial research revealed that the service we needed to upgrade was dependent on an internal gem. This gem used `ActiveRecord`, `ActiveSupport`, and `ActiveModel`, and was used by a few other services.

The first step was to upgrade this gem to support versions 5.2 to 7.0, making it backward compatible with other services. This was done incrementally. First, we added support for version 6.0, then 6.1, and finally 7.0.

Once this was accomplished, the actual work of upgrading our service to Rails 7 started.

### Upgrading the Service

We decided to do this incrementally as well. Upgrade the service from rails version 5.2 to 6.0 to 6.1 and finally to 7.0. Testing and deploying after every upgrade.

#### Upgrade service to rails version 6.0

The first step in this upgrade was to update the gems and dependencies supporting rails version 6.0. Great test coverage was an ally here, helping us make the changes confidently without the fear of breaking.

#### Failures encountered

- Failure caused due to the change in the behavior of the *where* clause.<br>
  **Cause**: Previous versions returned `ActiveRecord::RangeError` for the where clause after querying DB if the value was out of range. This behavior changed in rails version 6.0, so as to not run the query against out-of-range numbers and return an empty array instead.<br>
   **Resolution**: The test cases needed to change, in order to match the new expected result. No changes were required to the code.

More details on the [Rails 6 - RangeError not raised while interacting with ActiveRecord](https://github.com/rails/rails/issues/38309)

Once this change was complete, it was deployed to the staging environment and tested. It was then deployed to production.

#### Upgrade the ruby version to 2.7.0

Since Rails 6.1 requires ruby versions 2.5 and up, and Rails 7 requires ruby version 2.7 and up, the service was upgraded to ruby version 2.7 from version 2.5.

#### Upgrade service to rails version 7.0

Once the service was upgraded and deployed to production with rails 6.1, we started upgrading the service to 7.0. and this was where we encountered major failures.

#### Failures encountered

1. **Failure:** Unable to reload models/ReadOnly in initializers.<br>
   **Resolution:** Added `ActiveSupport::Reloader` to allow reloading the file.

2. **Failure:** Files under the *Concerns namespace* were not loading.<br>
   **Cause:** Applications that were running in *classic mode* needed to use *Zeitwerk mode* from Rails 7 onwards**.** Zeitwerk gem usage for rails 7.x changed how we define concerns.<br>
   **Resolution:** Removal of the Concerns module wrapping from file names fixed this issue.

3. **Failure**: Unable to resolve file names such as Author_ID<br>
   **Cause:** AuthorID was being resolved to author_i_d instead of author_id because of *Zeitwerk mode*.<br>
   **Resolution:** Adding inflections resolved the naming issues.<br>

#### Resolving Deprecation Warnings

1. **Warning message:** `Top level::CompositeIO is deprecated, require 'multipart/post' and use Multipart::Post::CompositeReadIO instead!`<br>
   **Cause:** Usage of an older version of the Faraday gem<br>
   **Resolution:** Updating faraday gem to version 1.x resolved this issue.

2. **Warning message:** Using legacy connection handling is deprecated. Please set **legacy_connection_handling** to **false** in your application<br>
   **Cause:** Update in connection management for rails > 6.1.<br>
   **Resolution:** Marking `config.active_record.legacy_connection_handling = false` resolved this issue. <br>
   Find more information on this [here](https://guides.rubyonrails.org/active_record_multiple_databases.html#migrate-to-the-new-connection-handling)

#### Failing CI build

**Failure:** `rake aborted! Don't know how to build task 'db:structure:load' (See the list of available tasks with rake --tasks). Did you mean?  db:test:load` <br>
**Cause:** `db:structure:load` deprecated in favor of `db:schema:load`. Structures and schemas both will be handled by` db:schema:load` <br>
**Resolution:** Updating commands to use `db:schema:load` in CI and locally, resolved this issue.<br>
Find more information on this [here](https://blog.saeloun.com/2020/09/30/rails-deprecates-db-structure-commands.html)