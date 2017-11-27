FROM thbeh/r-base:3.4.2

RUN apt-get update && apt-get install -y supervisor

COPY packages.R /tmp/
COPY scoreDrill.R /tmp/
COPY plumber.R /tmp/

RUN mkdir /code
ADD . /code/
ADD etc /etc

RUN Rscript /tmp/packages.R

EXPOSE 8000
## ENTRYPOINT ["R", "-e", "pr <- plumber::plumb(commandArgs()[4]); pr$run(host='0.0.0.0', port=8000)"]
## CMD ["/usr/local/lib/R/site-library/plumber/examples/04-mean-sum/plumber.R"]
CMD ["supervisord", "-c", "/etc/supervisord.conf"]

