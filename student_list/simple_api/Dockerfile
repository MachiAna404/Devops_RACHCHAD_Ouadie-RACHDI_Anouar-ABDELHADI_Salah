FROM nginx:alpine

LABEL maintainer="Abdelhadi_Rachdi_Rachchad <Rachchad_Rachdi_Abdelhadi@gmail.com>"

# Install Python and required dependencies
RUN apk add --no-cache python3 py3-pip libldap libpq libsasl py3-ldap

WORKDIR /

COPY student_age.py /
COPY student_age.json /data/student_age.json
COPY requirements.txt /

RUN pip3 install --no-cache-dir -r /requirements.txt

VOLUME /data

EXPOSE 3000

CMD ["python3", "./student_age.py"]