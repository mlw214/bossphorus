---
id: home
title: Bossphorus
sidebar_label: home
---

## Why use bossphorus?

*bossphorus* simplifies data-access patterns for data that do not fit into RAM. When you write a 100-gigabyte file, *bossphorus* automatically slices your dataset up to fit in bite-sized pieces.

When you request small pieces of your data for analysis, *bossphorus* intelligently serves only the parts you need, leaving the rest on disk.

## Usage

You can either run *bossphorus* using Python on your host machine, or use the provided Dockerfile to run *bossphorus* in a Docker container.

### Docker Method (Preferred)

#### 1. Build the docker image

```shell
docker build -t bossphorus .
```

#### 2. Create a directory for your filesystem to live in.

```shell
mkdir ./uploads
```

#### 3. Source the provided alias file.

This exposes a simplified wrapper to run *bossphorus* in a container.

```shell
source alias
```

#### 4. Run *bossphorus*!

```shell
bossphorus $(pwd)/uploads
```

You can run *bossphorus* in demo-mode by omitting the path to your uploads directory. **Data saved to bossphorus using this method will be destroyed when you end the bossphorus process!** Use only when testing *bossphorus* out.

### Native Method

```shell
pipenv install
mkdir ./uploads
python3 ./run.py
```

## Configuration

You can modify the top-level variables in `bossphorus/config.py` in order to change where bossphorus stores its data by default, and what size each file is by default.

A word of warning: While larger values of `BLOCK_SIZE` will reduce the amount of parallel threads in order to read a small file, it will also increase RAM usage per read. 256<sup>3</sup> is probably a good default, unless you have a very good reason to change it.

---

### Why bossphorus instead of other volumetric services?

That's a great question! *bossphorus* is certainly not the most performant, nor is it the most secure. And it's not versioned or distributed. If you're looking for a volumetric datastore, I would recommend looking below at the _Alternatives_ section for some really well-engineered systems.

The primary advantage of *bossphorus* is that it uses an identical API to that of [bossDB](https://bossdb.org) — and so if you anticipate your data growing from a few gigabytes now to a few terabytes later, you can get used to the bossDB ecosystem ([intern](https://https://github.com/jhuapl-boss/intern), [ingest](https://github.com/jhuapl-boss/ingest-client), and [many more tools](https://github.com/aplbrain/)) _now_, and then invest in real bossDB architecture later on with a seamless transition.

## Why is it called bossphorus?

*bossphorus* borrows its indexing pattern from _[bossDB](https://bossdb.org)_, a cloud-native database that can store way more data than *bossphorus* ever could. If your day-to-day routine includes multiple terabytes of volumetric data, [bossDB](https://bossdb.org) may be for you.

## Alternatives

| Project | Description |
|---------|-------------|
| [bossDB](https://bossdb.org) | Petabyte-scale, Cloud-Native Volumetric Database |
| [DVID](https://github.com/janelia-flyem/dvid) | Distributed, Versioned, Image-oriented Dataservice
