FROM nginx:latest
RUN rm /etc/nginx/conf.d/default.conf
RUN echo "	upstream loadbalancer {" > /etc/nginx/conf.d/load-balancer.conf
RUN echo "    server 172.18.0.2:80;" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "    server 172.18.0.3:80;" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "  }" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "  server {" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "    listen 80;" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "    location / {" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "      proxy_pass http://loadbalancer;" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "    }" >> /etc/nginx/conf.d/load-balancer.conf
RUN echo "  }" >> /etc/nginx/conf.d/load-balancer.conf
RUN nginx -t