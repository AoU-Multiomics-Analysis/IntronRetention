FROM mambaorg/micromamba:1.5.3

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    git \
    build-essential \
    make \
    g++ \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    ca-certificates \
    procps \
    && rm -rf /var/lib/apt/lists/*

RUN micromamba install -y -n base -c conda-forge -c bioconda \
    conda-forge::r-tidyverse \
    conda-forge::r-data.table \
    conda-forge::r-optparse \
    conda-forge::r-arrow \
    conda-forge::r-r.utils \
    conda-forge::r-bedr \
    bioconda::htslib \
    bioconda::bedtools \
    bioconda::samtools \
    bioconda::star=2.7.11b \
    && micromamba clean --all --yes

RUN wget -O /tmp/IRFinder.tar.gz \
    https://github.com/RitchieLabIGH/IRFinder/archive/refs/tags/v2.0.1.tar.gz && \
    mkdir -p /opt && \
    tar -xzf /tmp/IRFinder.tar.gz -C /opt && \
    mv /opt/IRFinder-2.0.1 /opt/IRFinder && \
    rm /tmp/IRFinder.tar.gz && \
    cd /opt/IRFinder && \
    if [ -f Makefile ]; then make; fi

ENV PATH="/opt/IRFinder/bin:/opt/IRFinder:/opt/conda/bin:${PATH}"

RUN STAR --version && \
    samtools --version | head -1 && \
    bedtools --version && \
    which IRFinder

CMD ["/bin/bash"]
