##################################################################################################
# authenticate your Docker client to your registry. Use the AWS CLI:(docker has to be pre installed)

#     aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 180294178330.dkr.ecr.us-east-1.amazonaws.com

#     Build your Docker image using the following command. 
#     docker build -t expense/frontend:v1 .

#     After the build is completed, tag your image so you can push the image to this repository:
#     docker tag expense/frontend:v1 180294178330.dkr.ecr.us-east-1.amazonaws.com/expense/frontend:v1

#     Run the following command to push this image to your newly created AWS repository:
#     docker push 180294178330.dkr.ecr.us-east-1.amazonaws.com/expense/frontend:v1
##################################################################################################

# creating lot of directories is because alpine image does not have the directories
# which nginx need during its process run ; but alpine version will not have by default 

FROM nginx:mainline-alpine3.20-slim
RUN rm -rf /etc/nginx/conf.d/* && \
    rm -rf /usr/share/nginx/html && \
    rm -rf /etc/nginx/nginx.conf && \
    mkdir -p /var/cache/nginx/client_temp && \
    mkdir -p /var/cache/nginx/proxy_temp && \
    mkdir -p /var/cache/nginx/fastcgi_temp && \
    mkdir -p /var/cache/nginx/uwsgi_temp && \
    mkdir -p /var/cache/nginx/scgi_temp && \
    chown -R nginx:nginx /var/cache/nginx && \
    chown -R nginx:nginx /etc/nginx/ && \
    chmod -R 755 /etc/nginx/ && \
    chown -R nginx:nginx /var/log/nginx && \
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid /run/nginx.pid
COPY nginx.conf /etc/nginx/nginx.conf 
COPY expense.conf /etc/nginx/default.d/expense.conf
COPY code /usr/share/nginx/html 
EXPOSE 80
USER nginx
# Run in foreground
CMD ["nginx", "-g", "daemon off;"]