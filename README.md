# RSS Feed Aggregator - Documentation

## Overview

This project is an RSS feed aggregator built using Go. It acts as a web server that allows clients to:

- Add RSS feeds to be collected.
- Follow and unfollow RSS feeds that other users have added.
- Fetch the latest posts from the RSS feeds you follow.

### What is RSS?

RSS (Really Simple Syndication) feeds allow websites to publish updates to their content in a standardized format. This project helps users stay updated with their favorite blogs, news sites, podcasts, and more.

## Features

- User Authentication: API key-based authentication is required for most endpoints.
- RSS Feed Management: Users can add, follow, and unfollow RSS feeds.
- Post Retrieval: Fetch the latest posts from followed feeds.
- Health Check Endpoint: Ensure the server is running and ready.

### Database

The project uses PostgreSQL as the database to store users, RSS feeds, follow relationships, and posts.

### Authentication

Most API endpoints require API key authentication. The API key should be included in the request headers as follows:

    Header Name: Authorization
    Header Value: ApiKey <your_api_key>

For example:

    makefile

    Authorization: ApiKey 375a367ccd776647af06f511db364c7a9c790ba89565cf65b759c7ac583e8cc1

### Environment Variables

The project uses environment variables to manage sensitive information. These are defined in the .env.template file, which serves as a guide to create your own .env file.
Required Environment Variables:

    DB_URL: The connection string for your PostgreSQL database.
    API_KEY: The API key used for authentication.

## API Endpoints
- Users

    Create User
        POST /v1/users
        Description: Register a new user.

    Get User
        GET /v1/users
        Description: Retrieve the authenticated user's information.
        Authentication: Required (API Key)

- Feeds

    Create Feed
        POST /v1/feeds
        Description: Add a new RSS feed to the system.
        Authentication: Required (API Key)

    Get Feeds
        GET /v1/feeds
        Description: Retrieve a list of all available RSS feeds.

- Feed Follows

    Get Followed Feeds
        GET /v1/feed_follows
        Description: Retrieve all RSS feeds that the authenticated user is following.
        Authentication: Required (API Key)

    Follow Feed
        POST /v1/feed_follows
        Description: Follow a new RSS feed.
        Authentication: Required (API Key)

    Unfollow Feed
        DELETE /v1/feed_follows/{feedFollowID}
        Description: Unfollow an RSS feed by providing the follow ID.
        Authentication: Required (API Key)

- Posts

    Get Posts
        GET /v1/posts
        Description: Retrieve the latest posts from the RSS feeds that the user is following.
        Authentication: Required (API Key)

- Health Check

    Readiness Check
        GET /v1/healthz
        Description: Check if the server is running and ready.

    Error Simulation
        GET /v1/err
        Description: Simulate an error for testing purposes.

## How to Run

To run this project, ensure that you have Go installed and a PostgreSQL instance running.

1. Clone the repository.
2. Create your .env file using the .env.template as a reference.
3. Install dependencies:
  ```bash
    go mod download
  ```
4. Build and run the server:
  ```bash
    go build && ./Blog-Aggregator
  ```

Feel free to contribute or suggest improvements!