[![PEP compatible](http://pepkit.github.io/img/PEP-compatible-green.svg)](http://pepkit.github.io)

# pifaces

This repository contains some [looper](http://looper.readthedocs.io) `pipeline_interface` files, so you can run basic utilities on your [PEP](http://pepkit.github.io) projects using looper.

## How it works

You can run any of these utilities on all samples of any [PEP-compatible project](http://pepkit.github.io) like so: 

1. Point your project at one of these pipeline_interface files (I usually use a subproject)
2. Specify the required sample attributes (by adding appropriate columns to your annotation)
3. Run `looper` (be sure to activate the subproject if you specified one)

## For example...

For example, to use the `rsync_piface.yaml` pipeline interface, add this to your `project_config.yaml`:

```{yaml}
subprojects:
  rsync:
    metadata:
      pipeline_interfaces: ${CODE}pifaces/rsync_piface.yaml
```

Then, add `src` and `dest` columns with filenames to your `sample_annotation` (these are what `rsync` needs), and then run with:

```
looper run project_config.yaml --sp rsync
```

This will run `rsync OLD NEW` for each sample in your project, allowing you to sync raw data from one file system to another, including remote syncing via SSH!

Now here's detailed documentation of what each task does and what it requires.

## Task `rsync`

*Task*: Runs rsync on files in your project for each sample, to sync remote data to a local file system (or vice versa), or to move files from one local filesystem to another.

*Required columns*: `src` specifies the source filename; `dest` specifies the destination.

## Task `filesize`

*Task*: Returns the file size (in bytes) for files for each sample.

*Required columns*: `file` specifying the path and filename to assess.
