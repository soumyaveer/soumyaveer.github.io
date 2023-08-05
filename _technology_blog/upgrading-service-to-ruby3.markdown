---
layout: post
title: Upgrading Services to Ruby version 3.1
date:  2023-08-04 19:00:00
categories: main
banner_image: "ruby-upgrade-3.jpeg"
---

Ruby released its 3.1 version on 25th Dec, 2021 and stopped supporting it's version 2.7 on March 31, 2023. A few of our services was on Ruby version 2.7 and hence was at the end of its life. We needed to upgrade our service to ruby 3.1 in order to stay compliant. This post talks about the steps we took for successful upgrade to ruby 3.1.    

### Step 1: Spike on dependencies
As a first step, we worked on figuring out what library or gem dependencies the service had that would need an update before we  update the service. As a result of this spike, we found two internal gems that would also need an upgrade.

### Step 2: Upgrade the dependencies
We first decided to start with the gem that was easiest to update and added support for Ruby 3.1 to it. But because multiple services were using this gem, we ensured support for ruby 2.7 and 3.1 and set up the tests to run in both the ruby versions. 

Once both the dependencies were updated, it was time to move on to the ruby upgrade of the Service.

### Step 3: Upgrade Users Service to support ruby version 3.1
Once we started working on the service, we encountered our main challenges.

1. **Incompatibility of keyword arguments in `ruby 3.1`**.

   If a method accepts keywords arguments, you had to use `**` to pass keywords instead of a hash. Or, if a method takes mixed arguments, you must pass arguments wrapped in a `{}`. <br><br>
    A snippet from the documentation -

    ```
   1. Using the last argument as keyword parameters is deprecated
   2. Passing the keyword argument as the last hash parameter is deprecated
   3. Splitting the last argument into positional and keyword parameters is deprecated
    ```

    From official ruby docs -
    ```
    “So when you want to pass keyword arguments, you should always use foo(k: expr) 
    or foo(**expr). If you want to accept keyword arguments, in principle, you 
    should always use def foo(k: default) or def foo(k:) or def foo(**kwargs).”
    ```

    **Short-term solution** Use [ruby2_keywords gem](https://github.com/ruby/ruby2_keywords), which would allow us to keep using the arguments as we were, but the official documentation states that they might remove the support for `rub2_keywords` once ruby 2.6 was EOL.

    **Final Solution:** The long-term solution was to make code changes. This had a tradeoff that it would be time-consuming because we had to update much of our codebase to make the changes compatible. We had time and did not want to revisit it again. So, we decided to handle the bull by its horns. 

2. **Error messages receiving a part of the backtrace along with the messages.**

   **Cause:** On investigation, we found that ruby 3.1 automatically included [error_highlight](https://github.com/ruby/error_highlight) as a dependency. By default, this behavior was causing the backtrace to be added to the error message.

   **Resolution:** Disable [error_highlight](https://github.com/ruby/error_highlight) to avoid adding a backtrace to the `error.message` method.

3. **The `rails server` command wasn't working anymore.**

   **Cause**: `gem webrick` was no longer automatically bundled for ruby versions >= 3.0.

   Snippet from official Ruby docs:
   ```
   The following libraries are no longer bundled gems or standard libraries. 
   Install the corresponding gems to use these features.
   - sdbm
   - webrick
   - net-telnet
   - xmlrpc
   ```

   **Resolution**:  Explicitly adding `gem webrick` to the Gemfile.

4. **Consumers were not able to consume the jobs created by the producers.** 

   **Cause**: A downstream dependency was converting the tube names from dashes to underscores, causing the failure of jobs. 
   
   **Resolution**: After much investigation, it was discovered that the downstream dependency got updated when we were updating the service. This dependency was causing the dashes to underscore conversions. To resolve this issue, we fixed the exact dependency version in the Gemfile of the service. 

After encountering and resolving all these challenges, the service was deployed successfully. 
