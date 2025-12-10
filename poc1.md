content/
├── learning-paths/              # Learning path definitions (JSON)
├── modules/
│   ├── metadata/                # Module metadata files (JSON)
│   └── units/                   # Unit content files (Markdown)
│       ├── module-1/            # Module 1 units
│       │   ├── unit-1.md
│       │   ├── unit-2.md
│       │   └── unit-3.md
│       └── module-2/            # Module 2 units
│           ├── unit-1.md
│           ├── unit-2.md
│           └── unit-3.md
└── assets/
    ├── images/                  # Upload images, static assets, and videos to blob storage (Script)
    └── videos/

.github/
└── workflows/                   # GitHub Actions workflows
    ├── content-validation.yml   # Automated content validation
    └── content-deployment.yml   # Content deployment pipeline

scripts/
├── validation/                  # Content validation scripts
│   ├── validate-metadata.py
│   ├── validate-links.py
│   └── validate-structure.py
└── deployment/                  # Deployment scripts
    └── deploy-to-cdn.py

docs/                            # Documentation
tests/                           # Automated tests
