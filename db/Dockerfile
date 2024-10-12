# MySQL Dockerfile
# Use the official MySQL image
FROM mysql:8.0

# Set environment variables for the MySQL root user password and database
ENV MYSQL_ROOT_PASSWORD=Mpr@399
ENV MYSQL_DATABASE=cwmsdb
# Copy initialization SQL file (optional)
COPY ./cwmsdb.sql /docker-entrypoint-initdb.d/

# Expose port 3306
EXPOSE 3306