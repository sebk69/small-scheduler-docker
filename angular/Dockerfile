FROM node:10

# install angular
RUN echo "install agular"
RUN npm install -g @angular/cli@10.2.4

# Build entrypoint
COPY idle.sh /home/node/idle.sh
RUN chown node:node /home/node/idle.sh
RUN chmod 755 /home/node/idle.sh

USER node

#ENTRYPOINT cd /webapp && ng serve --host 0.0.0.0
ENTRYPOINT /home/node/idle.sh
