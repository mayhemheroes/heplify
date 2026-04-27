FROM fuzzers/go-fuzz:1.2.0 as builder

ARG project='heplify'
ARG fuzzTargetPath='protos'

ADD . ${project}
WORKDIR ${project}
RUN GO_ENABLED=0 go-fuzz-build -libfuzzer -o /fuzz.a ./${fuzzTargetPath}
RUN clang -fsanitize=fuzzer /fuzz.a -o /fuzz.libfuzzer

FROM ubuntu:20.04
COPY --from=builder /fuzz.libfuzzer /
