ARG AGENCY_BASE_IMAGE=vcxagency-base:1.15.0
FROM ${AGENCY_BASE_IMAGE}

RUN npm install -g yarn

USER node
WORKDIR /home/node
COPY ./easy-indysdk ./easy-indysdk
COPY ./vcxagency-client ./vcxagency-client
COPY ./vcxagency-node ./vcxagency-node

USER root
RUN chown -R node:node /home/node

USER node
RUN yarn --cwd ./easy-indysdk install --production
RUN yarn --cwd ./vcxagency-client install --production
RUN yarn --cwd ./vcxagency-node install --production

LABEL org.label-schema.schema-version="1.1.0"
LABEL org.label-schema.name="vcxagency-node"
LABEL org.label-schema.description="Node VCX Agency"

ENV LOG_LEVEL ${LOG_LEVEL:-'true'}
ENV LOG_ENABLE_INDYSDK ${LOG_ENABLE_INDYSDK:-'false'}
ENV LOG_JSON_TO_CONSOLE ${LOG_JSON_TO_CONSOLE:-'true'}

EXPOSE ${SERVER_PORT}

CMD ["yarn", "--cwd", "vcxagency-node", "run", "serve"]
