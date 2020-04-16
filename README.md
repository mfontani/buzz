# buzz

... is the sound a [drone](https://drone.io/) makes.

This repository contains a `Dockerfile.alpine`, which is used to create/build a
`alpine`-based docker image which is then published, via github actions, to the
github package repository and on docker hub, at
[mfontani/buzz](https://hub.docker.com/r/mfontani/buzz)

The image is fairly lean, and it contains Just Enough for allowing a user to
perform common CI/CD operations, like using `curl` to fetch or trigger
something; use `ssh` and `git` to push or pull a repository; or use `ssh` and
`rsync` to publish changes somewhere.

It also contains `perl`, which is needed for `muffle-env` (as well as for
making some pipelines a lot easier to manage than with just bare `sh` and
`awk`).

The purpose of `muffle-env` is to help "muffle" environment variables which may
potentially be output by a pipeline step. By default, it "muffles" _all_
environment variables, but that's easily configurable by passing it a list of
regexes for which environment variable _names_ to muffle.

This can easily be used in a `.drone.yml` pipeline step to ensure `PLUGIN_*`
environment variables aren't output to the log _regardless_ of where they're
found, fixing a pet peeve of mine whereby a plugin for `git push`'ing or
`rsync`'ing changes would properly muffle with asterisks parts of the remote
server name or IP in the command's invocation, but the command itself would in
turn output the un-asterisked value.

# Author

Marco Fontani - <MFONTANI@cpan.org> - https://marcofontani.it/ - https://blog.darkpan.com/

# License

Copyright 2020 Marco Fontani <MFONTANI@cpan.org>

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
