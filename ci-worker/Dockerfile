FROM debian:latest
RUN apt-get update
RUN apt-get -y install git python3 python3-pip lsb-release curl gnupg2

#setup gcloud
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y

RUN apt-get update && apt-get install -y kubectl google-cloud-sdk google-cloud-sdk-app-engine-grpc google-cloud-sdk-pubsub-emulator google-cloud-sdk-app-engine-go google-cloud-sdk-cloud-build-local google-cloud-sdk-datastore-emulator google-cloud-sdk-app-engine-python google-cloud-sdk-cbt google-cloud-sdk-bigtable-emulator google-cloud-sdk-app-engine-python-extras google-cloud-sdk-datalab google-cloud-sdk-app-engine-java

RUN useradd -ms /bin/bash test
USER test
WORKDIR /home/test
RUN chown -R test:test /home/test

COPY --chown=test run_tests.sh /home/test/run_tests.sh
COPY --chown=test bucket_lifecycle.json /home/test/bucket_lifecycle.json
CMD /home/test/run_tests.sh
