# Creating diagrams

Create diagrams to convey information through charts and graphs

## About creating diagrams

You can create diagrams in Markdown using four different syntaxes: mermaid, geoJSON, topoJSON, and ASCII STL. Diagram rendering is available in GitHub Issues, GitHub Discussions, pull requests, wikis, and Markdown files.

## Creating Mermaid diagrams

Mermaid is a Markdown-inspired tool that renders text into diagrams. For example, Mermaid can render flow charts, sequence diagrams, pie charts and more. For more information, see the [Mermaid documentation](https://mermaid-js.github.io/mermaid/#/).

To create a Mermaid diagram, add Mermaid syntax inside a fenced code block with the `mermaid` language identifier. For more information about creating code blocks, see [Creating and highlighting code blocks](/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).

For example, you can create a flow chart by specifying values and arrows.

````text
Here is a simple flow chart:

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
````

![Screenshot of a rendered Mermaid flow chart with four lavender boxes labeled A, B, C, and D. Arrows extend from A to B, B to D, A to C, and C to D.](/assets/images/help/writing/mermaid-flow-chart.png)

> [!NOTE]
> You may observe errors if you run a third-party Mermaid plugin when using Mermaid syntax on GitHub.

### Checking your version of Mermaid

To ensure GitHub supports your Mermaid syntax, check the Mermaid version currently in use.

````text
```mermaid
  info
```
````

## Creating GeoJSON and TopoJSON maps

You can use GeoJSON or TopoJSON syntax to create interactive maps. To create a map, add GeoJSON or TopoJSON inside a fenced code block with the `geojson` or `topojson` syntax identifier. For more information, see [Creating and highlighting code blocks](/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).

### Using GeoJSON

For example, you can create a map by specifying coordinates.

````text
```geojson
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "id": 1,
      "properties": {
        "ID": 0
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
              [-90,35],
              [-90,30],
              [-85,30],
              [-85,35],
              [-90,35]
          ]
        ]
      }
    }
  ]
}
```
````

![Screenshot of a rendered GeoJSON map of the southeastern United States with a purple rectangular overlay over parts of Alabama and Mississippi.](/assets/images/help/writing/fenced-geojson-rendered-map.png)

### Using TopoJSON

For example, you can create a TopoJSON map by specifying coordinates and shapes.

````text
```topojson
{
  "type": "Topology",
  "transform": {
    "scale": [0.0005000500050005, 0.00010001000100010001],
    "translate": [100, 0]
  },
  "objects": {
    "example": {
      "type": "GeometryCollection",
      "geometries": [
        {
          "type": "Point",
          "properties": {"prop0": "value0"},
          "coordinates": [4000, 5000]
        },
        {
          "type": "LineString",
          "properties": {"prop0": "value0", "prop1": 0},
          "arcs": [0]
        },
        {
          "type": "Polygon",
          "properties": {"prop0": "value0",
            "prop1": {"this": "that"}
          },
          "arcs": [[1]]
        }
      ]
    }
  },
  "arcs": [[[4000, 0], [1999, 9999], [2000, -9999], [2000, 9999]],[[0, 0], [0, 9999], [2000, 0], [0, -9999], [-2000, 0]]]
}
```
````

![Screenshot of a rendered TopoJSON map of Indonesia, Singapore, and Malaysia with a blue point, a purple rectangular overlay, and blue zigzag lines.](/assets/images/help/writing/fenced-topojson-rendered-map.png)

For more information on working with `.geojson` and `.topojson` files, see [Working with non-code files](/en/repositories/working-with-files/using-files/working-with-non-code-files#mapping-geojsontopojson-files-on-github).

## Creating STL 3D models

You can use ASCII STL syntax directly in markdown to create interactive 3D models. To display a model, add ASCII STL syntax inside a fenced code block with the `stl` syntax identifier. For more information, see [Creating and highlighting code blocks](/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).

For example, you can create a simple 3D model:

````text
```stl
solid cube_corner
  facet normal 0.0 -1.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 1.0 0.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
  facet normal 0.0 0.0 -1.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 1.0 0.0 0.0
    endloop
  endfacet
  facet normal -1.0 0.0 0.0
    outer loop
      vertex 0.0 0.0 0.0
      vertex 0.0 0.0 1.0
      vertex 0.0 1.0 0.0
    endloop
  endfacet
  facet normal 0.577 0.577 0.577
    outer loop
      vertex 1.0 0.0 0.0
      vertex 0.0 1.0 0.0
      vertex 0.0 0.0 1.0
    endloop
  endfacet
endsolid
```
````

![Screenshot of a 3D model of a blue pyramid on a grid of black lines. Options "Wireframe", "Surface Angle", or "Solid" appear at bottom.](/assets/images/help/writing/fenced-stl-rendered-object.png)

For more information on working with `.stl` files, see [Working with non-code files](/en/repositories/working-with-files/using-files/working-with-non-code-files#3d-file-viewer).

---

```mermaid
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
```


