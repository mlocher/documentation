---
title: Using Elixir In CI/CD with Codeship Basic
shortTitle: Elixir
tags:
  - elixir
  - languages
menus:
  basic/languages:
    title: Elixir
    weight: 5
categories:
  - Languages And Frameworks    
---

* include a table of contents
{:toc}

## Versions And Setup

We currently don't have Elixir pre-installed on our build VMs so we'd recommend using our [Docker]({{ site.baseurl }}{% link pro/index.md %}) platform or downloading Elixir via the shell commands in your project's [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}).

The easiest way to do this is by using our [scripts repository](https://github.com/codeship/scripts), specifically the [Erlang](https://github.com/codeship/scripts/blob/master/languages/erlang.sh) and [Elixir](https://github.com/codeship/scripts/blob/master/languages/elixir.sh) scripts both. After connecting your repository, you can add these setup commands that will automatically download Elixir and Erlang. Both are needed to be able to run Elixir.

```shell
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/erlang.sh)"
source /dev/stdin <<< "$(curl -sSL https://raw.githubusercontent.com/codeship/scripts/master/languages/elixir.sh)"
```

The setup looks like this:
![Elixir Setup]({{ site.baseurl }}/images/languages/setupelixir.png)

## Dependencies

Installing dependencies via hex is supported once Elixir has been installed, as per the instructions above.

### Dependency Cache

We do not cache Elixir dependencies between builds.

## Frameworks And Testing

Elixir frameworks such as Phoenix, and test tools
such as ExUnit, are all supported on Codeship. Note that you will need to manually install all tools needed, in your project's [setup commands]({{ site.baseurl }}{% link _basic/quickstart/getting-started.md %}).

## Parallel Testing

If you are running [parallel test pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), you will want separate your tests into groups and call a group specifically in each pipeline. For instance:

**Pipeline 1:**
```shell
mix test tests/tests_1.exs
```

**Pipeline 2:**
```shell
mix test tests/tests_2.exs
```

### Parallelization Modules

In addition to parallelizing your tests explicitly [via parallel pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), some customers have found using ExUnit's built-in test parallelization is a good way to speed up your tests.

Note that aggressive parallelization can cause resource and build failure issues, as well.

## Notes And Known Issues

Due to Elixir version and build issues, you may find it helpful to tests your commands with different versions via an [SSH debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) if tests are running differently on Codeship compared to your local machine.
