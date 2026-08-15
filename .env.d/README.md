# User-level environment layout

The canonical local directory is:

  ~/.env.d/

Install the shared template locally with:

  mkdir -p ~/.env.d
  cp .env.template ~/.env.d/avatararts.env
  chmod 600 ~/.env.d/avatararts.env

Keep populated environment files outside Git. Use deployment secret stores for hosted services. The templates in this repository are documentation only and contain no live credentials.
