# lighttpd -centos7
FROM openshift/base-centos7

# Adicionar o mantenedor no metadado da imagem
LABEL maintainer="Glauber Donizeti Gasparotto Junior <juniorgasparotto@msn.com>"

# Variável de ambiente a respeito da aplicação utilzada
ENV LIGHTTPD_VERSION=1.4.53

# Labels utilizados pelo Openshift para descrever a imagem de construção
LABEL io.k8s.description="Platform for serving static HTML files" \
      io.k8s.display-name="Lighttpd 1.4.53" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,html,lighttpd"

# Instalar os pacotes necessários:
RUN yum install -y epel-release && yum install -y lighttpd && yum clean all -y

# Opcional: Copiar os arquivos de **build** das imagens
# COPY ./<builder_folder>/ /opt/app-root/

# Definir localização do binário s2i
LABEL io.openshift.s2i.scripts-url=image:///usr/libexec/s2i

# Copiar os binários do s2i para o diretório especificado
COPY ./s2i/bin/ /usr/libexec/s2i

# Copiar arquivo de configuração do lighttpd
COPY ./etc/ /opt/app-root/etc

# Alterar as permissões de /opt/app-root para o usuário 1001
RUN chown -R 1001:1001 /opt/app-root
RUN chown -R 1001:1001 /usr/libexec/s2i

# Utilizar o usuário 1001 criado na imagem base openshift/base-centos7
USER 1001

# Definir a porta utilizada pela aplicação
EXPOSE 8080

# Configurar o CMD padrão
CMD ["/usr/libexec/s2i/usage"]