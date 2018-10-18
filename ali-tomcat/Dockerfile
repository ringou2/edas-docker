FROM openjdk:8-jre-alpine

# Install required packages 
RUN apk add --no-cache \
    bash tzdata\
    su-exec

ENV ADMIN_USER=admin \
    APP_DIR=/edas \
    TIME_ZONE=Asia/Shanghai
ENV CATALINA_HOME $APP_DIR/taobao-tomcat-7.0.59
ENV PATH $CATALINA_HOME/bin:$PATH	
# Add a user and make dirs
RUN set -ex; \
    adduser -D "$ADMIN_USER"; \
    mkdir -p "$APP_DIR" ; \
    echo "${TIME_ZONE}" > /etc/timezone ;\
    ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime; 


RUN set -ex; \
    wget -q "http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/tomcat/taobao-tomcat-7.0.59.tgz?spm=a2c4g.11186623.2.12.6f1222b8GYtY9F&file=taobao-tomcat-7.0.59.tgz" -O taobao-tomcat-7.0.59.tgz; \
	wget -q "http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/pandora/unauth/taobao-hsf.tgz?spm=a2c4g.11186623.2.13.6f1222b8GYtY9F&file=taobao-hsf.tgz" -O taobao-hsf.tgz; \
    tar -xzf taobao-tomcat-7.0.59.tgz -C "$APP_DIR"/; \
	tar -xzf taobao-hsf.tgz -C "$APP_DIR"/taobao-tomcat-7.0.59/deploy/;\
    rm -rf taobao-hsf.tgz taobao-tomcat-7.0.59.tgz ; \
    chown -R "$ADMIN_USER:$ADMIN_USER" "$APP_DIR";    

WORKDIR $APP_DIR
VOLUME ["$APP_DIR"]
#USER $ADMIN_USER
EXPOSE 8080
CMD ["catalina.sh", "run"]
