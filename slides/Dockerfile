FROM node:12.13 AS base
WORKDIR /app
EXPOSE 8000

FROM alpine/git AS build
WORKDIR /src
RUN git clone https://github.com/hakimel/reveal.js.git .

FROM node:12.13 AS publish
WORKDIR /src
COPY init.sh .
RUN chmod u+x init.sh
COPY --from=build /src revealSrc
WORKDIR /src/revealSrc
RUN ../init.sh
COPY KeyNote.md .
COPY index.html .
COPY res/ .

FROM base AS final
WORKDIR /app
COPY --from=publish /src/revealSrc .
RUN npm install
CMD ["npm", "start"]
