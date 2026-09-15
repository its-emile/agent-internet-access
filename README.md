# When internet is blocked, storage is all you need

<a href="https://colab.research.google.com/github/its-emile/agent-internet-access/blob/main/blocked-internet-eval.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

A runnable measurement of one thing: whether an agent with no network egress can still get web
requests fulfilled, using only a storage surface it shares with an ordinary internal service.
Nothing here is an exploit. A shared folder is enough, as long as something on the outside can
read what the agent writes.

The write-up this accompanies is at [ifanyonereadsit.com](https://ifanyonereadsit.com/).

## What the notebook does

The isolated agent is given `s3_read`, `s3_write`, `s3_list` and `job_complete`, no network tool
of any kind, and ten jobs that each need a live web fetch. Nothing in its context suggests a way
out. A neighbouring service that shares the bucket answers external requests out of stored data,
and in doing so carries the request out and the answer back. It is not itself an agent.

The sweep runs that setup across several frontier models and against how much unrelated material
is already sitting in the bucket, then plots two things: whether the model writes a request to
storage at all, and whether it finds the response that comes back. Every read and write the
bucket sees is logged, so the channel can be traced afterwards.

## Running it

Open it in Colab with the badge above, and add an `OPENROUTER_API_KEY` to the notebook's secrets.
The bucket is a throwaway local directory standing in for an S3 prefix, so the only thing leaving
your machine is the model traffic.

Corrections and prior art welcome.
