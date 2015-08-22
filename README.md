This repo duplicates a problem that I was seeing running JRuby with
`guard-rspec`. (Specifically https://github.com/shoes/shoes4/issues/950)

I ran a similar minimal test for `guard-minitest`, and it didn't have the same
failure, so `guard-rspec` seemed a reasonable place to start given that.

To run the sample, clone this repo and run the following:

```
bundle exec guard -i -d
```

The effect seems to be:

  * First time I save the spec/test_spec.rb file, I don't see Guard to anything
  * Second time I save it, the tests will run, but then I get an error (appended below)
  * Subsequent saves don't seem to run anything at all.

Versions:

  * `jruby 1.7.20.1 (1.9.3p551) 2015-06-10 d7c8c27 on Java HotSpot(TM) 64-Bit Server VM 1.8.0_20-b26 [darwin-x86_64]`
  * `guard (2.13.0)`
  * `guard-rspec (4.6.4)`
  * `rspec (3.3.0)`
  * Mac OS X, 10.10.5

Log from failure:

```
22:31:28 - DEBUG - Notiffany: gntp not available (Please add "gem 'ruby_gntp'" to your Gemfile and run your app with "bundle exec".).
22:31:28 - DEBUG - Notiffany: growl not available (Please add "gem 'growl'" to your Gemfile and run your app with "bundle exec".).
22:31:28 - DEBUG - Notiffany: terminal_notifier not available (Please add "gem 'terminal-notifier-guard'" to your Gemfile and run your app with "bundle exec".).
22:31:28 - DEBUG - Notiffany: libnotify not available (Unsupported platform "darwin").
22:31:28 - DEBUG - Notiffany: notifysend not available (Unsupported platform "darwin").
22:31:28 - DEBUG - Notiffany: notifu not available (Unsupported platform "darwin").
22:31:28 - DEBUG - Command execution: {"ALTERNATE_EDITOR"=>"false"} emacsclient --eval '1'
22:31:28 - DEBUG - Notiffany: emacs not available (Emacs client failed).
22:31:28 - DEBUG - Notiffany: tmux not available (:tmux notifier is only available inside a TMux session.).
22:31:28 - DEBUG - Notiffany: file not available (No :path option given).
22:31:28 - DEBUG - Notiffany is using TerminalTitle to send notifications.
The signal USR1 is in use by the JVM and will not work correctly on this platform
22:31:28 - DEBUG - Guard starts all plugins
22:31:28 - DEBUG - Hook :start_begin executed for Guard::RSpec
22:31:28 - INFO - Guard::RSpec is running
22:31:28 - DEBUG - Hook :start_end executed for Guard::RSpec
22:31:28 - INFO - Guard is now watching at '/Users/jclark/source/jruby-guard-rspec'
22:31:28 - DEBUG - Guards jobs done. Sleeping...

# At this point I did the first save...
22:31:33 - DEBUG - Sleep interrupted by events.
22:31:33 - DEBUG - Guards jobs done. Sleeping...

# At this point I did the second save...
22:31:38 - DEBUG - Sleep interrupted by events.
22:31:38 - DEBUG - Hook :run_on_modifications_begin executed for Guard::RSpec
22:31:38 - INFO - Running: spec/test_spec.rb
.

Finished in 0.128 seconds (files took 1.47 seconds to load)
1 example, 0 failures

22:31:41 - ERROR - Guard::RSpec failed to achieve its <run_on_modifications>, exception was:
> [#] Errno::ECHILD: No child processes - No child processes
> [#] org/jruby/RubyProcess.java:728:in `waitpid2'
> [#] org/jruby/RubyProcess.java:777:in `wait2'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:39:in `_really_run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:28:in `_run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:53:in `_without_bundler_env'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/bundler-1.10.3/lib/bundler.rb:245:in `with_clean_env'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/bundler-1.10.3/lib/bundler.rb:232:in `with_original_env'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/bundler-1.10.3/lib/bundler.rb:238:in `with_clean_env'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:53:in `_without_bundler_env'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:27:in `_run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/rspec_process.rb:16:in `initialize'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/runner.rb:68:in `_really_run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/runner.rb:57:in `_run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec/runner.rb:41:in `run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec.rb:42:in `run_on_modifications'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec.rb:48:in `_throw_if_failed'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-rspec-4.6.4/lib/guard/rspec.rb:42:in `run_on_modifications'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:82:in `_supervise'
> [#] org/jruby/RubyKernel.java:1274:in `catch'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:79:in `_supervise'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:61:in `run_on_changes'
> [#] org/jruby/RubyHash.java:1341:in `each'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:56:in `run_on_changes'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:119:in `_run_group_plugins'
> [#] org/jruby/RubyArray.java:1613:in `each'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:117:in `_run_group_plugins'
> [#] org/jruby/RubyKernel.java:1274:in `catch'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:116:in `_run_group_plugins'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:54:in `run_on_changes'
> [#] org/jruby/RubyArray.java:1613:in `each'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/runner.rb:53:in `run_on_changes'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/internals/queue.rb:23:in `process'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/commander.rb:43:in `start'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/cli/environments/valid.rb:16:in `start_guard'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/cli.rb:122:in `start'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/thor-0.19.1/lib/thor/command.rb:27:in `run'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/thor-0.19.1/lib/thor/invocation.rb:126:in `invoke_command'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/thor-0.19.1/lib/thor.rb:359:in `dispatch'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/thor-0.19.1/lib/thor/base.rb:440:in `start'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/aruba_adapter.rb:32:in `execute'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/lib/guard/aruba_adapter.rb:19:in `execute!'
> [#] /Users/jclark/.rbenv/versions/jruby-1.7.20.1/lib/ruby/gems/shared/gems/guard-2.13.0/bin/_guard-core:11:in `(root)'
22:31:41 - INFO - Guard::RSpec has just been fired
22:31:41 - DEBUG - Guards jobs done. Sleeping...
```
