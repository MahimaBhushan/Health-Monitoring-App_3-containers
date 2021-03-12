FROM python:3.7
WORKDIR /usr/src/app
 
COPY callbacks.py .
COPY layouts.py .
COPY app.py .
COPY assets /usr/src/app/assets 
COPY index.py .
COPY db.py .
 
COPY requirements.txt .
EXPOSE 5555
RUN pip install -r requirements.txt
CMD ["python","./index.py"]
