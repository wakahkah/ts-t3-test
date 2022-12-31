# Ts-t3-test App

---

# Table of Contents

[T3 Framework](#t3-framework)
[Supabase](#supabase)
[NextAuth Discord](#nextauth-discord)
[Prisma Migrate](#prisma-migrate)
[Vercel Deploy](#vercel-deploy)

---

## [T3 Framework](https://create.t3.gg/)

#### Requirement

- {"node":">=14.17"}

#### Create App

```sh
npm create t3-app@latest
```

## [Supabase](https://supabase.com/)

#### Setup Steps:

1. Use github login
2. New project & generate db pwd
3. Make sure docker installed in local development env (https://supabase.com/docs/guides/resources/supabase-cli/local-development)
4. Use cmd `npx supabase login` to login
5. Follow [url](https://app.supabase.com/account/tokens) to gen token and copy it back to cmd
6. Init supabase `npx supabase init`
7. Start supabase `npx supabase start` (several container is running on docker)
8. Go to [local dashboard](http://localhost:54323) to check the local status
9. Get Supabase Cloud db url
   a. Go Back to supabase current project portal
   b. Click setting button on left menu
   c. click database(project setting)
   d. Copy connection string (uri)
   e. Write it down with the password
10. Copy following cmd to env file DATA_SOURCE
    Default URL:
    `postgresql://postgres:postgres@localhost:54322/postgres`
11. Update src code (prisma/scherma.prisrma) provider value to `postgresql`
12. Uncomment all “@db.Text”
13. Run cmd: `npx prisma db push`
14. You can check the update of db with [local dashboard](localhost:54323)

## [NextAuth Discord](https://discord.com/developers/applications)

#### Setup Steps:

1. Login discord account
2. Generate secret
   a. Go to oauth2
   b. Generate client secret
   c. Copy to discord client secret
3. Add redirects to OAuth2:

```
http://localhost:3000/api/auth/callback/discord
https://ts-t3-test.vercel.app/api/auth/callback/discord
```

4. Run the application to test on local `npm run dev`
5. Try to login on (http://localhost:3000)

## Prisma Migrate

#### Steps:

1. Migrate with name “initial migration” in localhost `npx prisma migrate dev --name initial_migration`
   **_There is a bug of supabase that cannot do this migrate job, need to build another db using docker or use another exist db_**
2. Commit the changes to github

## [Vercel Deploy](https://vercel.com/)

#### Steps:

1. Login [Vercel](https://vercel.com/new) using github
2. Add github account to repo
3. Import the project
4. Update build command `prisma generate && prisma migrate deploy && next build`
5. Config project: add all env value on .env to environment variable session
   _Database URL must use supabase on cloud_
6. Click "deploy"
7. Try the [Webiste](https://ts-t3-test.vercel.app/)
