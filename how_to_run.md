# Data Engineering Assignment

## Use your own API keys. All API keys hardcoded are not real. For illustration purposes only.

## Description
This project involves processing and analyzing scraped data using PySpark, Redis, and Neo4j. The aim is to store, process, and analyze text data efficiently.
Import the .backup file into Neo4J if you just want to see the nodes.
There are 10104 nodes/words in the backup file.

![Image](https://github.com/Brynlai/Data-Engineering-Assignment-RDSY2S2/blob/main/LexNeo4J%20-%20Copy.png)

## Usage

### Starting Services
0. Open Powershell in Administrator mode and run wsl:
    ```bash
    wsl ~
    ```
1. Start Hadoop and Spark services:
   ```bash
   start-dfs.sh
   ```
   ```bash
   start-yarn.sh
   ```
2. Start Kafka and Zookeeper:
   > Note: Wait for about 30 seconds before performing the next step.
   ```bash
   zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties &
   ```
   ```bash
   kafka-server-start.sh $KAFKA_HOME/config/server.properties &
   ```
    

3. Switch to student:
    ```bash
    su - student
    ```
### Running Notebooks (Curently not working if ru scrape_article while consumer is running.)
1. Activate the virtual environment and start Jupyter Lab:
   ```bash
   source de-prj/de-venv/bin/activate
   jupyter lab
   ```
   
2. Open 2 Powershell Terminals from Windows, then go (de-venv) student@R2D3:~/urdirectory$
3. (To show kafka working) cd into the directory both files are in!
    - Producer Terminal:
       ```bash
       python kafka_producer_show.py
        ```
   - Consumer Terminal:
       ```bash
        spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.13:3.5.1 kafka_consumer_show.py
        ```
     > [!IMPORTANT]  
        DO NOT RUN 
        "$ python kafka_producer_show.py"
        when scrape_aritcles_into_words.ipynb or neo4j.ipynb is running.
        "kafka_consumer_show.py" can run in the background. 

4. Run the notebooks in this sequence:
   - `scrape_articles_into_words.ipynb`
   - `neo4j.ipynb`


### Stopping Services

1. Stop Kafka and Zookeeper:
   > Note: Wait for about 30 seconds before performing the next step.
   ```bash
   kafka-server-stop.sh
   ```
   ```bash
   zookeeper-server-stop.sh
   ```
3. Stop Hadoop and Spark services:
   ```bash
   stop-yarn.sh
   ```
   ```bash
   stop-dfs.sh
   ```

