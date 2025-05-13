1. Téléchargez ou copiez le contenu du fichier Docker Compose de la plateforme Confluent en mode KRaft

   ```bash
    wget https://raw.githubusercontent.com/MohamedKaraga/cfbs/refs/heads/main/docker-compose.yml
   ```

2. Analysez le fichier Docker Compose
3. Démarrez le cluster Kafka avec l'option -d pour l'exécuter en mode détaché:
   ```bash
   docker-compose up -d broker akhq
   ```
   
4. Affichez les conteneurs en cours d'exécution

   ```bash
   docker-compose ps
   ```
   
5. Exécuter dans la console du conteneur `broker`
   ```bash
   docker-compose exec broker /bin/bash
   ```
   
**_Exécutez la commande suivante dans la console du conteneur `broker`_**

6. Créer le topic `cfbs`:
   ```bash
   kafka-topics --bootstrap-server kafka:9092 \
   --create \
   --partitions 1 \
   --replication-factor 1 \
   --topic cfbs
   ```   
   
7. Exécutez `kafka-console-producer` pour produire un message dans le topic `cfbs`:
   ```bash
   kafka-console-producer --bootstrap-server kafka:9092 --topic cfbs
   ```
   Exemple

   ```bash
   > Hello, DJIN :)
   > This is a test message.
   > Another message.
   ``` 
     
8. Exécutez `kafka-console-consumer` pour consommer dans le topic `cfbs`:
   ```bash
   kafka-console-consumer \
   --bootstrap-server kafka:9092 \
   --from-beginning \
   --topic cfbs
   ```
9. Arrêter le cluster Kafka avec l'option -v pour supprimer les volumes

   ```bash
   docker-compose down -v
   ```
