FROM python

COPY main.py main.py
COPY requirements.txt requirements.txt
RUN pip3 install -r ./requirements.txt



ENTRYPOINT ["python3", "main.py"]