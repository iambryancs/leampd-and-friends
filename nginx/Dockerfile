#
#+++++++++++++++++++++++++++++++++++++++++++++++
# Image setup
#+++++++++++++++++++++++++++++++++++++++++++++++
#

FROM nginx
LABEL maintainer="Bryan CS <yanser25@gmail.com>"

#
#+++++++++++++++++++++++++++++++++++++++++++++++
# Config setup
#+++++++++++++++++++++++++++++++++++++++++++++++
#
ADD config/default.conf /etc/nginx/conf.d

ARG APPLICATION_ROOT=/
RUN if [ "${APPLICATION_ROOT}" != "/" ]; then \
	# Update conf
	sed -i 's@/html@/html'"${APPLICATION_ROOT}"'@g' \ 
	/etc/nginx/conf.d/default.conf \
;fi

EXPOSE 80
