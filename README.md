# Denkwerk Knooppuntenanalyse (Network Analysis)

<img src="https://denkwerk.online/media/1152/weerbaarheid_transparant_mockup.png?width=500&height=281.25" alt="Weerbaarheid by Design Report Cover" width="200" align="right" style="margin-left: 20px;">

This is the frontend visualization tool for the DenkWerk report "Weerbaarheid by Design - De vijf principes voor een weerbaar Nederland". The tool analyzes how threats interconnect and identifies central nodes that strengthen or cause other threats, providing insights for targeted interventions.

[See the full report](https://denkwerk.online/media/1155/weerbaarheid-by-design.pdf)

![Final Threat Graph](public/graaf_volledig.svg)

*The final graph of relationships between all threats considered. Explore it on the [hosted version of this repository](https://denkwerk-kickstartai.nl/knooppuntenanalyse).*

## Features

The tool provides an interactive network visualization using a custom-modified Reagraph library with WebGL rendering. The network displays identified national threats, where directed edges from threat A to threat B indicate that our methodology has discovered a significant volume of supporting citations linking these threats. For detailed information about the backend methodology, see the [report's appendix B](https://denkwerk.online/media/1156/weerbaarheid-by-design-appendix.pdf).

The analysis employs a directed Eigenvector Centrality algorithm to identify critical threat interconnections and highlight the most influential nodes within the network. Users can filter nodes by threat categories and explore both the network structure and its underlying citation data through an integrated tutorial system. The tool also includes additional example visualizations to demonstrate the approach and broader context.

## Technology Stack

- Frontend: React + TypeScript
- Visualization: Custom Reagraph library (WebGL-based network graphs)
- Styling: Tailwind CSS + shadcn/ui components
- Build Tool: Vite

## Project Structure

### Core Application (`/src`)

- `/components/layout/` - Main layout and supporting visualization components
  - `NarrativeLayout.tsx` - Primary application layout
  - `CentralNodeExample.tsx` - Example visualization demonstrating central node analysis
  - `TraditionalRiskMatrix.tsx` - Example risk matrix visualization
  - `TransformerAttentionVisualizer.tsx` - Example attention mechanism visualization

- `/components/visualization/` - Visualization components
  - `MainContent.tsx` - Main visualization container
  - `GraphChart.tsx` - Primary graph visualization
  - `NodeSelector.tsx` - Node filtering interface
  - `ColorLegend.tsx` - Color coding legend
  - `ThreatTable.tsx` - Tabular threat data display
  - `TutorialOverlay.tsx` - Interactive tutorial system

- `/components/visualization/networkGraph/` - Network analysis logic
  - `networkService.ts` - Core network data processing
  - `networkFetcher.ts` - Data fetching utilities
  - `eigenvectorCentrality.ts` - Centrality calculations
  - `threatImpactService.ts` - Threat analysis
  - `types.ts` - TypeScript definitions

- `/components/visualization/relationGraph/` - Relationship visualization (Interactive visualization supporting the main networkGraph)
  - `RelationGraphCanvas.tsx` - Relation-specific graph rendering
  - `GraphCanvas.tsx` - Base graph canvas component
  - `EdgeLine.tsx` - Edge rendering + interactivity component
  - `HierarchicalLayout.ts` - Contains the algorithm to sort this graph hierarchically

- `/components/ui/` - Reusable UI components (shadcn/ui)

### Network Analysis Library (`/reagraph`)

- Vendored copy of the Reagraph library with direct modifications
- Note: Due to time constraints, this is not a proper fork but rather a "dirty" modification of the original library
- The library has been copied directly into the project and modified in place for specific requirements
- Custom modifications include:
  - Added gradient color styling for edges
  - Made edges clickable for interaction
- Key features:
  - WebGL-powered rendering for high performance
  - Custom node and edge styling
  - Interactive selection and highlighting
  - Camera controls and scene management

### Data Files (`/public`)

- `nodes.json` - Network node data (from backend)
- `edges.json` - Network edge data (from backend)
- `threat_impact.json` - Threat impact analysis data (from methodology)

## Installation & Setup

1. Clone the repository
   ```bash
   git clone https://github.com/ICascha/knooppuntenanalyse-tool
   cd denkwerk-knooppuntenanalyse
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Start development server
   ```bash
   npm run dev
   ```

4. Build for production
   ```bash
   npm run build
   ```

5. Preview production build
   ```bash
   npm run preview
   ```

## Data Format

### Nodes (nodes.json)
```json
{
  "id": "unique-node-id",
  "label": "Display Name",
  "summary": "Node description",
  "category": "Category Name",
  "citaten": [...],
  "nr_docs": 10,
  "nr_citations": 25
}
```

### Edges (edges.json)
```json
{
  "id": "unique-edge-id",
  "source": "source-node-id",
  "target": "target-node-id",
  "weight": 1.0,
  "raw_count": 5,
  "citaat_relaties": [...]
}
```

## Acknowledgments

This project utilizes a vendored copy of the [Reagraph](https://github.com/reaviz/reagraph) library, a high-performance WebGL network graph visualization component for React. Reagraph is an open-source project created by the team at [Reaviz](https://reaviz.dev/).