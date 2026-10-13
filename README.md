## Architettura a microservizi per il Monitoraggio di Voli (Distributed Systems and Big Data)

Progetto sviluppato per il corso di **Sistemi Distribuiti e Big Data (A.A. 2025/26)** presso l'Università di Catania (Studenti: Alessia Fichera, Davide Pantò). 
Il sistema implementa un'architettura a microservizi resiliente e containerizzata per il monitoraggio in tempo reale 
dei dati di volo tramite l'integrazione con l'API OpenSky Network.

## 🚀 Architettura e Tecnologie Principali
- **Microservizi & Containerizzazione:** Sviluppo di microservizi indipendenti (`UserManager` e `DataCollector`) interamente containerizzati con **Docker**.
- **Orchestrazione:** Gestione del cluster locale tramite **Kubernetes (Kind - Kubernetes IN Docker)** con mappatura delle porte e deployment scalabili.
- **API Gateway & Routing:** Utilizzo di **Nginx** come punto di ingresso unico per mascherare la complessità di rete e instradare le richieste REST.
- **Comunicazione Inter-servizio:** Scambio dati bidirezionale e sincrono tramite protocollo **gRPC**.
- **Messaging Asincrono:** Integrazione di **Apache Kafka** (pattern Producer-Consumer) per disaccoppiare la raccolta dati dalla pipeline di alerting.
- **Resilienza:** Implementazione del pattern **Circuit Breaker** per la gestione dei guasti verso l'API esterna OpenSky e strategie di fallback automatico.
- **Persistenza & Caching:** Database relazionali dedicati (`UserDB` e `DataDB` in MySQL)[cite: 23] affiancati da **Redis** per la deduplicazione delle richieste e la gestione della semantica *At-Most-Once*.
- **Monitoraggio (White-box):** Integrazione di **Prometheus** per lo scraping periodico di metriche applicative custom (latenze, contatori di traffico e performance) esposte dai microservizi.
