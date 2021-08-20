# GitHub API
Most of these require `jq` and `curl`.

## User Information
```
curl https://api.github.com/users/CHANGEME
```

Example output:
```json
{
  "login": "torvalds",
  "id": 1024025,
  "node_id": "MDQ6VXNlcjEwMjQwMjU=",
  "avatar_url": "https://avatars.githubusercontent.com/u/1024025?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/torvalds",
  "html_url": "https://github.com/torvalds",
  "followers_url": "https://api.github.com/users/torvalds/followers",
  "following_url": "https://api.github.com/users/torvalds/following{/other_user}",
  "gists_url": "https://api.github.com/users/torvalds/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/torvalds/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/torvalds/subscriptions",
  "organizations_url": "https://api.github.com/users/torvalds/orgs",
  "repos_url": "https://api.github.com/users/torvalds/repos",
  "events_url": "https://api.github.com/users/torvalds/events{/privacy}",
  "received_events_url": "https://api.github.com/users/torvalds/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Linus Torvalds",
  "company": "Linux Foundation",
  "blog": "",
  "location": "Portland, OR",
  "email": null,
  "hireable": null,
  "bio": null,
  "twitter_username": null,
  "public_repos": 6,
  "public_gists": 0,
  "followers": 140639,
  "following": 0,
  "created_at": "2011-09-03T15:26:22Z",
  "updated_at": "2021-07-19T18:38:01Z"
}
```

## Clone all of a user's repos
```sh
#!/bin/sh

if [ ! $1 ]; then
    echo usage $0 github_username
    exit 1
fi

count=$(curl -s https://api.github.com/users/$1 | jq '.public_repos')

if [ -z "$count" ] || [ "$count" = "null" ]; then
    echo error
    exit
fi

x=1
while [ $count -gt 0 ]; do
    for repo in $(curl -s "https://api.github.com/users/$1/repos?&per_page=100&page=$x" | jq '.[].clone_url'); do
	git clone $(echo "$repo" | tr -d \")
    done
    x=$(($x + 1))
    count=$(($count - 100))
done
```

## Download all releases
```sh
#!/bin/sh

if [ ! $1 ]; then
    echo usage $0 username/repo
    exit
fi

for i in $(curl -s "https://api.github.com/repos/$1/releases" | jq '.[].assets[].browser_download_url'); do
    # lol @ curl and wget
    wget -x $(echo $i | tr -d \")
done
```

## List user's starred repos
```sh
#!/bin/sh

# https://gist.github.com/sebble/e5af3d03700bfd31c62054488bfe8d4f

if [ ! $1 ]; then
    echo usage $0 github_username
    exit 1
fi

count=$(curl -sI "https://api.github.com/users/$1/starred?per_page=1" | grep "^link:" | egrep -o 'page=[0-9]+' | tail -n 1 | cut -d = -f 2)

if [ -z "$count" ] || [ "$count" = "null" ]; then
    echo error
    exit
fi

x=1
while [ $count -gt 0 ]; do
    for repo in $(curl -s "https://api.github.com/users/$1/starred?&per_page=100&page=$x" | jq '.[].clone_url'); do
	echo "$repo"
    done
    x=$(($x + 1))
    count=$(($count - 100))
done
```
