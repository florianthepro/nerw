flowchart TB
    subgraph ClientA["Node A / Quelle"]
        SeedA["Master Seed"]
        IdentityA["Identity Key Pair"]
        SessionA["Ephemeral Session Key Pair"]
        CacheA["Lokaler Request-Cache"]
        AppA["Browser / Anwendung / lokaler Resolver"]

        SeedA -->|"deterministische Ableitung"| IdentityA
        IdentityA -->|"autorisiert"| SessionA
        AppA --> CacheA
    end

    subgraph Registry["Dezentrale Registry-Blockchain"]
        Chain["Finalisierte Registry"]
        State["Aktueller State Root"]
        Names["Domain → Identity Public Key"]
        Sessions["Identity Key → gültige Session Keys"]
        Rotation["Key-Rotation und Widerruf"]
        Expiry["Domain-Ablauf und Verlängerung"]

        Chain --> State
        Chain --> Names
        Chain --> Sessions
        Chain --> Rotation
        Chain --> Expiry
    end

    subgraph Overlay["Dezentrales Request- und Routing-Overlay"]
        Node1["Node / Validator 1"]
        Node2["Node / Validator 2"]
        Node3["Node / Validator 3"]
        Node4["Node / Validator 4"]

        Pool1["TTL Request Pool"]
        Pool2["TTL Request Pool"]
        Pool3["TTL Request Pool"]
        Pool4["TTL Request Pool"]

        Node1 --- Node2
        Node2 --- Node3
        Node3 --- Node4
        Node4 --- Node1
        Node1 --- Node3

        Node1 --> Pool1
        Node2 --> Pool2
        Node3 --> Pool3
        Node4 --> Pool4
    end

    subgraph ServerZ["Node Z / Ziel"]
        SeedZ["Master Seed"]
        IdentityZ["Identity Key Pair"]
        SessionZ["Ephemeral Session Key Pair"]
        EndpointZ["Lokaler Endpoint Manager"]
        ServiceZ["DNS / Web / anderer Dienst"]

        SeedZ -->|"deterministische Ableitung"| IdentityZ
        IdentityZ -->|"autorisiert"| SessionZ
        EndpointZ --> ServiceZ
    end

    AppA -->|"1. Domain abfragen"| Names
    Names -->|"2. Z Identity Public Key + Proof"| AppA

    SessionA -->|"3. signierter Locate Request"| Node1
    Node1 -->|"Gossip mit TTL"| Node2
    Node1 -->|"Gossip mit TTL"| Node3
    Node2 -->|"Gossip mit TTL"| Node4

    Node4 -->|"4. Request erreicht Ziel"| SessionZ
    SessionZ -->|"5. verschlüsselte Locate Response"| Node4
    Node4 --> Node2
    Node2 --> Node1
    Node1 --> SessionA

    SessionA <-->|"6. authentifizierter Handshake"| SessionZ
    AppA <-->|"7. Ende-zu-Ende verschlüsselte Verbindung"| ServiceZ
