# 或者指定你自己build好的镜像
FROM php:7.2-fpm
#
# .... 自身项目PHP环境配置 ... 建议直接基于已经 build 好的镜像
#

# 增加 TINI (这里直接使用二进制 也可以使用镜像对应的包管理安装）
ENV TINI_VERSION v0.17.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

# COPY composer
ENV COMPOSER_ALLOW_SUPERUSER 1
# 在镜像中增加 composer
COPY --from=composer:1.6 /usr/bin/composer /usr/bin/composer
COPY --from=composer:1.6 /docker-entrypoint.sh /composer-entrypoint.sh
WORKDIR /app
ENTRYPOINT ["/composer-entrypoint.sh"]
CMD ["composer"]