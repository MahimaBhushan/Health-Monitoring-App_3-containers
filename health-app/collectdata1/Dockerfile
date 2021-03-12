FROM python:3.7
WORKDIR /usr/src/app
 
COPY collect_data_10.py .
COPY requirements.txt .
 
RUN pip install -r requirements.txt
CMD ["python","./collect_data_10.py", "10.64.97.111", "bigbend", "bigbend123"]
 