FROM alpine:3.1

# Update
RUN apk add --update python py-pip

# Install app dependencies
RUN pip install Flask

EXPOSE  8000
WORKDIR /code
CMD ["python", "app.py", "-p 5000"]

