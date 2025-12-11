# Repo Structure Documentation

```plaintext
geneis/
├── .github/
│   └── workflows/
│       ├── ci.yml                    # Run tests on PR
│       ├── deploy-web.yml            # Deploy web app
│       ├── deploy-api.yml            # Deploy API
│       └── deploy-mobile.yml         # Build mobile apps
│
├── apps/
│   ├── web/                          # Next.js web application
│   │   ├── public/
│   │   ├── src/
│   │   │   ├── app/                  # Next.js App Router
│   │   │   │   ├── (auth)/           # Route group: auth pages
│   │   │   │   │   ├── login/
│   │   │   │   │   └── register/
│   │   │   │   ├── (main)/           # Route group: main app
│   │   │   │   │   ├── photos/
│   │   │   │   │   ├── albums/
│   │   │   │   │   ├── search/
│   │   │   │   │   └── settings/
│   │   │   │   ├── share/[token]/    # Public sharing
│   │   │   │   ├── layout.tsx
│   │   │   │   └── page.tsx
│   │   │   ├── components/           # Web-specific components
│   │   │   │   ├── gallery/
│   │   │   │   │   ├── PhotoGrid.tsx
│   │   │   │   │   ├── PhotoViewer.tsx
│   │   │   │   │   └── InfiniteGallery.tsx
│   │   │   │   ├── upload/
│   │   │   │   │   ├── UploadButton.tsx
│   │   │   │   │   ├── UploadProgress.tsx
│   │   │   │   │   └── DragDropZone.tsx
│   │   │   │   ├── albums/
│   │   │   │   │   ├── AlbumCard.tsx
│   │   │   │   │   └── AlbumGrid.tsx
│   │   │   │   └── search/
│   │   │   │       ├── SearchBar.tsx
│   │   │   │       └── SearchResults.tsx
│   │   │   ├── lib/                  # Web utilities
│   │   │   │   ├── api-client.ts     # tRPC/fetch wrapper
│   │   │   │   ├── upload.ts         # Upload logic
│   │   │   │   └── image-utils.ts
│   │   │   ├── hooks/                # React hooks
│   │   │   │   ├── usePhotos.ts
│   │   │   │   ├── useUpload.ts
│   │   │   │   └── useInfiniteScroll.ts
│   │   │   └── styles/
│   │   │       └── globals.css
│   │   ├── next.config.js
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   ├── mobile/                       # React Native (Expo)
│   │   ├── app/                      # Expo Router
│   │   │   ├── (tabs)/               # Tab navigation
│   │   │   │   ├── index.tsx         # Photos tab
│   │   │   │   ├── albums.tsx        # Albums tab
│   │   │   │   ├── search.tsx        # Search tab
│   │   │   │   └── profile.tsx       # Profile tab
│   │   │   ├── (auth)/
│   │   │   │   ├── login.tsx
│   │   │   │   └── register.tsx
│   │   │   ├── photo/[id].tsx        # Photo viewer
│   │   │   └── _layout.tsx
│   │   ├── components/
│   │   │   ├── PhotoGrid.tsx
│   │   │   ├── PhotoViewer.tsx
│   │   │   ├── UploadButton.tsx
│   │   │   └── CameraButton.tsx
│   │   ├── lib/
│   │   │   ├── api-client.ts
│   │   │   ├── background-upload.ts
│   │   │   ├── camera.ts
│   │   │   └── permissions.ts
│   │   ├── hooks/
│   │   │   ├── usePhotos.ts
│   │   │   ├── useBackgroundUpload.ts
│   │   │   └── useCameraRoll.ts
│   │   ├── app.json
│   │   ├── eas.json                  # Expo build config
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   └── api/                          # Backend API (Go or Node.js)
│       ├── cmd/
│       │   └── server/
│       │       └── main.go           # Entry point
│       ├── internal/
│       │   ├── config/
│       │   │   └── config.go         # Environment config
│       │   ├── auth/
│       │   │   ├── jwt.go
│       │   │   ├── middleware.go
│       │   │   └── service.go
│       │   ├── photos/
│       │   │   ├── handler.go        # HTTP handlers
│       │   │   ├── service.go        # Business logic
│       │   │   ├── repository.go     # Database queries
│       │   │   └── models.go         # Domain models
│       │   ├── albums/
│       │   │   ├── handler.go
│       │   │   ├── service.go
│       │   │   └── repository.go
│       │   ├── search/
│       │   │   ├── handler.go
│       │   │   ├── service.go
│       │   │   └── meilisearch.go
│       │   ├── storage/
│       │   │   ├── r2.go             # Cloudflare R2 client
│       │   │   └── s3.go             # S3-compatible interface
│       │   ├── processing/
│       │   │   ├── image.go          # Image processing
│       │   │   ├── exif.go           # EXIF extraction
│       │   │   └── queue.go          # Job queue
│       │   ├── ml/
│       │   │   ├── faces.go          # Face detection
│       │   │   ├── labels.go         # Object detection
│       │   │   └── embeddings.go     # Vector embeddings
│       │   └── database/
│       │       ├── postgres.go
│       │       ├── migrations/
│       │       │   ├── 001_init.sql
│       │       │   ├── 002_add_faces.sql
│       │       │   └── 003_add_embeddings.sql
│       │       └── queries/          # SQL queries
│       │           ├── photos.sql
│       │           └── albums.sql
│       ├── pkg/                      # Public packages
│       │   ├── httputil/
│       │   ├── errors/
│       │   └── validator/
│       ├── tests/
│       │   ├── integration/
│       │   └── unit/
│       ├── go.mod
│       ├── go.sum
│       ├── Dockerfile
│       └── README.md
│
├── packages/                         # Shared packages
│   ├── types/                        # TypeScript types (shared)
│   │   ├── src/
│   │   │   ├── photo.ts
│   │   │   ├── album.ts
│   │   │   ├── user.ts
│   │   │   └── api.ts                # API request/response types
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   ├── ui/                           # Shared React components
│   │   ├── src/
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Modal.tsx
│   │   │   ├── Avatar.tsx
│   │   │   └── index.ts
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   ├── config/                       # Shared configs
│   │   ├── eslint-config/
│   │   │   ├── index.js
│   │   │   └── package.json
│   │   ├── tsconfig/
│   │   │   ├── base.json
│   │   │   ├── nextjs.json
│   │   │   ├── react-native.json
│   │   │   └── package.json
│   │   └── tailwind-config/
│   │       ├── index.js
│   │       └── package.json
│   │
│   └── utils/                        # Shared utilities
│       ├── src/
│       │   ├── date.ts               # Date formatting
│       │   ├── file.ts               # File size, validation
│       │   ├── image.ts              # Image utilities
│       │   └── constants.ts          # Shared constants
│       ├── tsconfig.json
│       └── package.json
│
├── services/                         # Microservices/Workers
│   ├── image-processor/              # Image processing worker
│   │   ├── src/
│   │   │   ├── index.ts
│   │   │   ├── processor.ts          # Sharp.js processing
│   │   │   ├── queue.ts              # Redis queue consumer
│   │   │   └── storage.ts            # Upload to R2
│   │   ├── Dockerfile
│   │   ├── tsconfig.json
│   │   └── package.json
│   │
│   ├── ml-worker/                    # ML/AI worker (Python)
│   │   ├── src/
│   │   │   ├── main.py
│   │   │   ├── face_detection.py
│   │   │   ├── object_detection.py
│   │   │   ├── embeddings.py
│   │   │   └── queue_consumer.py
│   │   ├── models/                   # ML model files
│   │   ├── requirements.txt
│   │   ├── Dockerfile
│   │   └── README.md
│   │
│   └── search-indexer/               # Meilisearch indexer
│       ├── src/
│       │   ├── index.ts
│       │   ├── indexer.ts
│       │   └── meilisearch.ts
│       ├── tsconfig.json
│       └── package.json
│
├── infrastructure/                   # IaC and deployment
│   ├── terraform/
│   │   ├── modules/
│   │   │   ├── database/
│   │   │   ├── storage/
│   │   │   └── compute/
│   │   ├── environments/
│   │   │   ├── dev/
│   │   │   ├── staging/
│   │   │   └── production/
│   │   └── main.tf
│   ├── docker/
│   │   ├── docker-compose.yml        # Local development
│   │   ├── docker-compose.prod.yml
│   │   └── nginx/
│   │       └── nginx.conf
│   └── kubernetes/                   # If using K8s
│       ├── deployments/
│       ├── services/
│       └── ingress/
│
├── scripts/                          # Utility scripts
│   ├── setup-dev.sh                  # Setup local env
│   ├── seed-db.ts                    # Seed test data
│   ├── migrate.ts                    # Run migrations
│   ├── generate-types.ts             # Generate types from DB
│   └── backup.sh                     # Backup script
│
├── docs/                             # Documentation
│   ├── api/
│   │   ├── openapi.yml               # API spec
│   │   └── README.md
│   ├── architecture/
│   │   ├── diagrams/
│   │   └── decisions/                # Architecture Decision Records
│   │       ├── 001-monorepo.md
│   │       ├── 002-storage.md
│   │       └── 003-ml-approach.md
│   └── setup/
│       ├── local-development.md
│       └── deployment.md
│
├── .husky/                           # Git hooks
│   ├── pre-commit
│   └── pre-push
│
├── .vscode/                          # VSCode settings
│   ├── settings.json
│   ├── extensions.json
│   └── launch.json
│
├── turbo.json                        # Turborepo config
├── package.json                      # Root package.json
├── pnpm-workspace.yaml               # PNPM workspaces
├── .gitignore
├── .env.example
├── README.md
└── LICENSE
```
