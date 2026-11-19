![Rugby](https://user-images.githubusercontent.com/449385/218269381-8f8cd682-139a-40c0-be7b-76376de3752f.svg)

# Rugby (legacy server)

The original Ruby server for [Rugby](https://github.com/superhighfives/rugby), a GIF-powered music video by my band Brightly. It matched each lyric to GIFs from Giphy and cached them in Memcached.

Status: retired. Made in 2015 and ran on Heroku. It was replaced by [rugby-server](https://github.com/superhighfives/rugby-server), a Cloudflare Workers port with the same data format.

## Running it

You'll need Ruby 1.9, Bundler, Memcached and a Giphy API key.

```sh
bundle
cp sample.env .env               # add your Giphy key
memcached &
bundle exec foreman start
bundle exec foreman run ruby scripts/fetch.rb   # refresh the cached GIFs
```

## How it works

- `app.rb` is a Sinatra app that serves the lyrics and their GIFs as JSON or JSONP.
- `lib/lyrics.rb` holds the lyrics, timings and search keywords. `lib/gif_searcher.rb` queries Giphy and `lib/gif_cache.rb` stores the results.
- `scripts/fetch.rb` and `scripts/flush.rb` refresh and clear the cache. On Heroku, `fetch.rb` ran on the Scheduler add-on.

## License

This code (not including the lyrics) is licensed under a [Creative Commons Attribution License](http://creativecommons.org/licenses/by/3.0/): you may use it, but you must give attribution.
