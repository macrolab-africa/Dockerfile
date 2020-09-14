# variable
ARG VERSION=3.1
# download SDK image from dockerHub
FROM mcr.microsoft.com/dotnet/core/sdk:${VERSION} AS publish-env

# set the working directory
WORKDIR /dist

# copy all projects files to the images : COPY src_path dest_path
COPY . .
# download all dependencies in the SDK image
RUN dotnet restore
# publish the application to /dist/out - dist is the workdir
RUN dotnet publish -c Release -o out

#Download the runtime - this is the image that host the application
FROM mcr.microsoft.com/dotnet/core/aspnet:${VERSION}
# set defaut app directory
WORKDIR /app
#copy published files from the SDK image to runtime
COPY --from=publish-env /dist/out .

EXPOSE 80

ENTRYPOINT ["dotnet","BookStore.dll"]

#ENTRYPOINT ["dotnet", "BookStore.dll"]
#to run the container - two command are required
#CMD1: docker build -t containerName .
#CMD2: docker run -d -p 44366:80/tcp --name container_name image_name



