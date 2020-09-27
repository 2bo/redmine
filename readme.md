# cloneしてcheckout
git co -b code_reading

# dockerfileの追加
cp Dockerfile ../redmine/
cp docker-compose.yml ../redmine/
cp ../rails6-on-docker/entrypoint.sh /

# config/database.ymlの設定

# Dockerの環境構築
docm build
dcom run --rm web bunle install
dcom run web --rm bundle exec rake generate_secret_token
docker-compose run --rm web rake db:create
docker-compose run --rm web bin/bundle exec rake db:migrate
docker-compose run --rm web bin/bundle exec rake redmine:load_default_data
