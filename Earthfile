FROM alpine:3.13

fib:
    ARG N
    IF [ "$N" -le 1 ]
        RUN echo "$N" > data
    ELSE
        COPY --build-arg N="$(expr $N - 1)" +fib/data data1
        COPY --build-arg N="$(expr $N - 2)" +fib/data data2
        RUN expr "$(cat data1)" + "$(cat data2)" > data
    END
    SAVE ARTIFACT data

run:
    COPY --build-arg N=0 +fib/data fib-0
    COPY --build-arg N=1 +fib/data fib-1
    COPY --build-arg N=2 +fib/data fib-2
    COPY --build-arg N=3 +fib/data fib-3
    COPY --build-arg N=4 +fib/data fib-4
    COPY --build-arg N=5 +fib/data fib-5
    RUN test "$(cat fib-0)" = "0"
    RUN test "$(cat fib-1)" = "1"
    RUN test "$(cat fib-2)" = "1"
    RUN test "$(cat fib-3)" = "2"
    RUN test "$(cat fib-4)" = "3"
    RUN test "$(cat fib-5)" = "5"
    RUN echo finished
