
```mermaid

graph TD
    subgraph Data_Acquisition ["Data Acquisition & Preprocessing"]
        A[Sentinel-2 L2A Imagery] --> B[Cloud & Atmospheric Correction]
        B --> C[Vegetation Indexing <br/>NDVI/SAVI]
        C --> D[Patch Generation & Normalization]
    end

    subgraph Model_Core ["ViT-Deep SVDD Core"]
        D --> E[Patch Embedding & Positional Encoding]
        E --> F[Transformer Encoder Stack]
        F -- "Self-Attention" --> G[Global Feature Representation]
        G --> H[Deep SVDD Head]
    end

    subgraph Inference_Output ["Inference & Interpretation"]
        H --> I{Calculate Distance R}
        I -- "Distance > Threshold" --> J[Anomaly Detected]
        I -- "Distance <= Threshold" --> K[Normal Vegetation]
        J --> L[Grad-CAM / Attention Rollout]
        L --> M[Anomaly Localization Heatmap]
    end

    style Model_Core fill:#000000,stroke:#4a148c,stroke-width:2px
    style Data_Acquisition fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style Inference_Output fill:#fff3e0,stroke:#e65100,stroke-width:2px

