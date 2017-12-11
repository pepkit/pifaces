# pifaces

This repository contains some [looper](http://looper.readthedocs.io) `pipeline_interface` files, so you can run basic utilities on your looper projects.

## How it works

You can run any of these actions on all samples of any [PEP-compatible project](http://pepkit.github.io) like so: 

1. Point your project at one of these pipeline_interface files (I usually use a subproject)
2. Specify the required sample attributes (by adding appropriate columns to your annotation)
3. Run `looper` (be sure to activate the subproject if you specified one)

So, for example, add this to your `project_config.yaml`:

```{yaml}
subprojects:
  rsync:
    metadata:
      pipeline_interfaces: ${CODE}pifaces/rsync.yaml
```

Then, add `from` and `to` columns with filenames to your `sample_annotation` (these are what `rsync` needs), and then run with:

```
looper run project_config.yaml --sp rsync
```

This will run `rsync OLD NEW` for each sample in your project, allowing you to sync raw data from one file system to another, including remote syncing via SSH!

Now here's detailed documentation of what each task does and what it requires.

## `rsync.yaml`

*Task*: Run rsync on files in your project for each sample

*Required columns*: `from` specifies the source filename; `to` specifies the destination
