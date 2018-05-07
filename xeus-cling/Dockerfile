FROM buildpack-deps:artful
RUN apt-get update &&     apt-get install --yes --no-install-recommends locales &&     apt-get purge &&     apt-get clean &&     rm -rf /var/lib/apt/lists/*
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen &&     locale-gen
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV SHELL /bin/bash
ARG NB_USER=parsa
ARG NB_UID=1000
ENV USER ${NB_USER}
ENV HOME /home/${NB_USER}
RUN adduser --disabled-password     --gecos "Default user"     --uid ${NB_UID}     ${NB_USER}
WORKDIR ${HOME}
RUN apt-get update &&     apt-get install --yes --no-install-recommends        less        npm        unzip        && apt-get purge &&     apt-get clean &&     rm -rf /var/lib/apt/lists/*
EXPOSE 8888
ENV APP_BASE /srv
ENV CONDA_DIR ${APP_BASE}/conda
ENV NB_PYTHON_PREFIX ${CONDA_DIR}
ENV PATH ${CONDA_DIR}/bin:${PATH}
COPY conda/install-miniconda.bash /tmp/install-miniconda.bash
COPY conda/environment.frozen.yml /tmp/environment.yml
RUN bash /tmp/install-miniconda.bash && rm /tmp/install-miniconda.bash /tmp/environment.yml
USER root
COPY src/ ${HOME}
RUN chown -R ${NB_USER}:${NB_USER} ${HOME}
USER ${NB_USER}
RUN conda env update -n root -f "environment.yml" && conda clean -tipsy && conda list -n root
USER ${NB_USER}
CMD ["jupyter", "notebook", "--ip", "0.0.0.0"]
USER root
ENV BINDER_URL=http://mybinder.org/v2/gh/QuantStack/xeus-cling/0.2.0-binder
ENV REPO_URL=https://github.com/QuantStack/xeus-cling
RUN cd /tmp  && wget -q https://github.com/jupyterhub/mybinder.org-deploy/archive/ce31915cfc76b749a4e089b7c105856cea545319.tar.gz -O appendix.tar.gz  && tar --wildcards -xzf appendix.tar.gz --strip 1 */appendix  && ./appendix/run-appendix  && rm -rf appendix.tar.gz appendix
USER $NB_USER