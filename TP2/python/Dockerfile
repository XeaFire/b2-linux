FROM debian:bullseye-slim

RUN apt-get update && apt-get install -y python3 python3-pip

RUN pip3 install ./requirements.txt

COPY main.py main.py

ENTRYPOINT ["python3", "main.py"]