graph TD
    %% Subgraph 1: Data Acquisition
    subgraph Data_Acquisition ["Data Acquisition & Preprocessing"]
        A[Sentinel-2 L2A Imagery] --> B[Cloud & Atmospheric Correction]
        B --> C[Vegetation Indexing <br/><i>NDVI / SAVI</i>]
        C --> D[Patch Generation & Normalization]
    end

    %% Subgraph 2: Model Core
    subgraph Model_Core ["ViT-Deep SVDD Core"]
        D --> E[Patch Embedding & <br/>Positional Encoding]
        E --> F[Transformer Encoder Stack]
        F -- "Self-Attention" --> G[Global Feature Representation]
        G --> H[Deep SVDD Head]
    end

    %% Subgraph 3: Inference
    subgraph Inference_Output ["Inference & Interpretation"]
        H --> I{Calculate <br/>Distance R}
        I -- "Distance > Threshold" --> J[<b>Anomaly Detected</b>]
        I -- "Distance <= Threshold" --> K[Normal Vegetation]
        J --> L[Grad-CAM / <br/>Attention Rollout]
        L --> M[Anomaly Localization <br/>Heatmap]
    end

    %% Styling
    style Data_Acquisition fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style Model_Core fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style Inference_Output fill:#fff3e0,stroke:#e65100,stroke-width:2px
    
    %% Node Specific Styling
    style J fill:#ffcdd2,stroke:#b71c1c
    style K fill:#c8e6c9,stroke:#1b5e20
