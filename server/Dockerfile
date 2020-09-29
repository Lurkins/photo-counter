FROM python:3.8.5-slim-buster
ENV VIRTUAL_ENV=/opt/venv 
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"
COPY requirements.txt .
RUN pip install -r requirements.txt 
COPY app.py .
EXPOSE 5000
CMD [ "python", "app.py" ] 