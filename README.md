# elasticsearch-with-django-mongoengine
Installation and Usage of Elasticsearch with mongoengine and django


############### Elasticsearch Installation Commands #################

sudo apt install default-jre

sudo apt install openjdk-11-jre-headless

sudo apt install openjdk-8-jre-headless 

java -version

echo $JAVA_HOME

sudo apt-get install apt-transport-https

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

sudo apt-get update && sudo apt-get install elasticsearch

###################### Setting of Elastic search ###############

sudo nano /etc/elasticsearch/elasticsearch.yml

action.auto_create_index: .monitoring*,.watches,.triggered_watches,.watcher-history*,.ml*,-l*,+z

##################### end ################


#Enable/Start Service

sudo /bin/systemctl enable elasticsearch.service

sudo systemctl start elasticsearch.service

systemctl status elasticsearch.service

sudo systemctl start elasticsearch.service

systemctl status elasticsearch.service

curl -X GET "http://localhost:9200/?pretty"

sudo apt install curl  # curl not install

curl -X GET "http://localhost:9200/?pretty"


######################### Create Elasticsearch Indices/Index for mongodb ###########################

from elasticsearch import Elasticsearch

es = Elasticsearch(timeout=30, max_retries=10, retry_on_timeout=True)

ex_list = []

for ex in Example.objects.filter():

    b = {}
    b["id"] = ex.id
    b["name"] = ex.name
    ex_list.append(b)
    
es.indices.create(index='example_list', ignore=400)  # Create the index 

es.index(index="example_list", id=2, doc_type="example_list", body={"data": ex_list}) # populate the data to index

#es.indices.delete(index='example_list', ignore=400) # remove existing index


#########################Usage Indices/Index for mongodb ###########################

from elasticsearch import Elasticsearch

es = Elasticsearch()

data_list = es.get(index="example_list",doc_type="example_list", id=2)['_source']['data']


