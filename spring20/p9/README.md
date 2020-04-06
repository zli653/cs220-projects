# Project 9: Amazon Reviews

## Clarifications/Corrections/Hints:
* **(4/4/2020, 5:25 pm)** Bugs in data.zip and test.py fixed. Redownload if you have already downloaded.

## Introduction

In this project, you'll be analyzing a collection of reviews of Amazon products (adapted from https://www.kaggle.com/datafiniti/consumer-reviews-of-amazon-products/data).
This data is messy!  You'll face the following challenges:

* data is spread across multiple files
* some files will be CSVs, others JSONs
* the files may be missing values or be too corrupt to parse

Due to the COVID-19 situation, P9 will have 30 questions instead of the usual 40. The questions have been
split up into two stages with an additional optional stage for those who want some practice.

In stage 1, you'll write code to cleanup the data, representing
everything as Review objects (you'll create a new type for these).  In
stage 2, you'll analyze your clean data.

## Setup

**Step 1:** download `data.zip` and extract it to a directory on your
computer (using [Mac directions](http://osxdaily.com/2017/11/05/how-open-zip-file-mac/) or
[Windows directions](https://support.microsoft.com/en-us/help/4028088/windows-zip-and-unzip-files)).

**Step 2:** download `test.py` to the directory from step 1 (`test.py` should be next to the `data` directory, not in it)

**Step 3:** create a `main.ipynb` in the same location.  Do all work for both stages there, and turn it in when complete.

Note: Make sure `data`, `main.ipynb` and `test.py` are in same directory.  Otherwise getting the tests to pass on your machine only will not be a good indication of whether they'll pass when we run them with the files organized as such.


## The Stages

* [Stage 1](stage1.md): parse a mix of CSV and JSON files to get Review objects
* [Optional](optional_questions.md): additional optional questions for practice
* [Stage 2](stage2.md): analyze the reviews of the Amazon products

## Linting

We are now introducing linting as a way to help you write better code. Please check it out
and try running it on your code! Everything you need to know to get started is explained
[here](../../linter/README.md).
