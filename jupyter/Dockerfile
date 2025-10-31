FROM spark:3.5.7
USER root
RUN set -eux; \
    apt-get update; apt-get install -y --no-install-recommends python3 python3-pip tini; \
    pip3 install --no-cache-dir jupyterlab notebook ipykernel pandas findspark; \
    ln -sf /usr/bin/python3 /usr/bin/python; \
    # nối py4j để tiện set PYTHONPATH
    ln -sf "$(ls /opt/spark/python/lib/py4j*-src.zip | head -n1)" /opt/spark/python/lib/py4j.zip; \
    rm -rf /var/lib/apt/lists/*
ENV SPARK_HOME=/opt/spark
ENV PYSPARK_PYTHON=/usr/bin/python3
ENV PYTHONPATH=/opt/spark/python:/opt/spark/python/lib/py4j.zip
WORKDIR /work
ENTRYPOINT ["/usr/bin/tini","--"]
CMD ["jupyter","lab","--ip=0.0.0.0","--port=8888","--no-browser","--IdentityProvider.token=dev","--allow-root"]
