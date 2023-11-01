FROM node:latest


RUN apt-get update && \
    apt-get install -y xvfb xsel && \
    rm -rf /var/lib/apt/lists/*


RUN npm install -g @nocturne-xyz/nocturne-setup


RUN echo '#!/bin/bash' > /start.sh && \
    echo 'Xvfb :99 -screen 0 1280x960x24 &' >> /start.sh && \
    echo 'export DISPLAY=:99' >> /start.sh && \
    echo 'exec "$@"' >> /start.sh && \
    chmod +x /start.sh

ENTRYPOINT ["/start.sh"]
CMD ["/bin/bash"]
