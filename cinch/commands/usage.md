---
layout: default
title: usage
parent: commands
grand_parent: Cinch
nav_order: 1
---
All cinch commands follow the [docopt](http://docopt.org/){:target="_default"} standard. They all require
that the first argument is `project_name` argument, excluding `help` and `list`. In addition, there are a set of
global options.

{: .note}
Remember that arguments are different than options. As such, the first argument can occur after
options: `cinch create --working-dir=/home/andrew project_name`

```php
/**
 * @throws Exception
 */
protected function execute(InputInterface $input, OutputInterface $output): int
{
    $projectName = $input->getArgument('project');
    $target = $input->getArgument('target');
    $history = $input->getOption('history') ?: $target;
    $targetName = $input->getOption('target-name') ?? $projectName;

    $changelog = new Uri($input->getOption('changelog'));
    if (!$changelog->getScheme())
        $changelog = $changelog->withScheme('file'); // fs changelog is just a path

    $project = new Project(
        new ProjectName($projectName),
        new TargetUri($targetName, $target),
        new Uri($history),
        $changelog
    );

    $this->logger->info("creating project");
    $this->createProject->execute($project);

    /* move temp log to project log dir, now that project dir exists */
    (new Filesystem())->rename($this->tempLogFile, "$this->projectDir/log/" . basename($this->tempLogFile));

    return self::SUCCESS;
}
```

# Global Options

* `--target-name` This overrides project file's `defaultTarget`
* `--working-dir`

----

[Symfony Console]: https://symfony.com/doc/current/components/console.html