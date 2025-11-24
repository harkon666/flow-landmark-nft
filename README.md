# Flow Landmark NFT 🌊

A decentralized social event platform built on Flow blockchain where users can create, attend events, mint NFT moments, and collect accessories through gacha mechanics.

## 🌟 Features

### Event Management
- **Create Events**: Organize online/offline events with customizable details
- **Event Registration**: Users can register for events on-chain
- **Check-in System**: Verify attendance with blockchain-backed check-ins
- **Event Passes**: NFT-based passes that serve as tickets

### NFT System
- **Moment NFTs**: Capture and mint memorable moments as NFTs
- **Free Mint**: First-time users get one free moment mint
- **Event Pass Redemption**: Convert event passes into moment NFTs
- **Accessory System**: Equip/unequip accessories to customize moment NFTs

### Marketplace
- **NFT Trading**: Buy and sell moments and accessories
- **Storefront Integration**: Powered by NFTStorefrontV2
- **Listing Management**: Create, cancel, and manage listings

### Gacha & Collectibles
- **Gacha Packs**: Purchase mystery accessory packs
- **Reveal Mechanics**: Open packs to discover accessories
- **Accessory Collection**: Build your collection of unique items

### Social Features
- **User Profiles**: Customizable profiles with bio, images, and social links
- **Moment Feed**: Browse and discover moments from the community
- **Likes & Comments**: Engage with content
- **Featured Content**: Highlight favorite moments and passes

## 🛠 Tech Stack

### Frontend
- **React 19** - UI framework
- **TypeScript** - Type safety
- **TanStack Router** - File-based routing
- **TanStack Query** - Data fetching & caching
- **Tailwind CSS 4** - Styling
- **Motion (Framer Motion)** - Animations
- **@onflow/react-sdk** - Flow blockchain integration
- **Magic Link** - Email-based authentication
- **Vite** - Build tool

### Backend
- **Go 1.24** - Server language
- **Echo** - Web framework
- **Ent** - Entity framework for database ORM
- **PostgreSQL** - Database
- **Swagger** - API documentation
- **Flow Go SDK** - Flow blockchain interaction

### Smart Contracts
- **Cadence** - Flow blockchain smart contract language
- Contracts for:
  - NFTMoment (moments)
  - NFTAccessory (accessories)
  - EventManager (event management)
  - EventPass (event tickets)
  - UserProfile (user profiles)
  - AccessoryPack (gacha system)

## 📋 Prerequisites

- **Node.js** >= 18
- **Go** >= 1.24
- **PostgreSQL** >= 14
- **Flow CLI** (for Cadence development)
- **Bun** or **npm** (package manager)

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/harkon666/flow-landmark-nft.git
cd flow-landmark-nft
```

### 2. Environment Setup

#### Backend Environment Variables

Create `/backend/.env`:

```env
DATABASE_URL=postgres://user:password@localhost:5432/flowlandmark?sslmode=disable
PORT=8000
FLOW_NETWORK=testnet
PINATA_JWT=your_pinata_jwt_here
```

#### Frontend Environment Variables

Create `/frontend/.env`:

```env
VITE_BASE_URL=http://localhost:8000
VITE_MAGIC_PUBLISHABLE_KEY=your_magic_publishable_key
```

### 3. Database Setup

```bash
# Create PostgreSQL database
createdb flowlandmark

# The schema will be auto-created by Ent on first run
```

### 4. Backend Setup

```bash
cd backend

# Install dependencies
go mod download

# Run database migrations (auto via Ent)
# The schema will be created automatically when you run the app

# Start the API server
go run ./api

# In another terminal, start the indexer
go run ./indexer
```

The backend will:
- API server runs on `http://localhost:8000`
- Indexer subscribes to Flow blockchain events
- Swagger docs available at `http://localhost:8000/swagger/index.html`

### 5. Frontend Setup

```bash
cd frontend

# Install dependencies
bun install
# or: npm install

# Start development server
bun run dev
# or: npm run dev
```

Frontend runs on `http://localhost:5173`

## 📁 Project Structure

```
flow-landmark-nft/
├── backend/
│   ├── api/              # REST API handlers & routes
│   ├── config/           # Configuration files
│   ├── ent/              # Ent schema & generated code
│   │   └── schema/       # Database entity definitions
│   ├── indexer/          # Blockchain event indexer
│   ├── transactions/     # Go wrappers for Cadence transactions
│   ├── utils/            # Utility functions & event processors
│   └── swagdto/          # Swagger DTO definitions
├── frontend/
│   ├── src/
│   │   ├── components/   # React components
│   │   │   ├── cards/    # Card components
│   │   │   ├── modals/   # Modal dialogs
│   │   │   └── profile/  # Profile-related components
│   │   ├── hooks/        # Custom React hooks
│   │   │   ├── api/      # API data fetching hooks
│   │   │   ├── auth/     # Authentication hooks
│   │   │   └── transactions/ # Blockchain transaction hooks
│   │   ├── routes/       # File-based routes (TanStack Router)
│   │   ├── providers/    # React context providers
│   │   └── lib/          # Utility libraries & configs
├── cadence/
│   ├── contracts/        # Smart contracts
│   ├── scripts/          # Read-only scripts
│   └── transactions/     # State-changing transactions
└── flow.json             # Flow configuration
```

## 🔑 Key Components

### Smart Contracts

| Contract | Description |
|----------|-------------|
| `NFTMoment` | Main NFT for user moments with equippable accessories |
| `NFTAccessory` | Accessories that can be equipped on moments |
| `EventManager` | Event creation, registration, and check-in |
| `EventPass` | NFT-based event passes |
| `UserProfile` | On-chain user profile management |
| `AccessoryPack` | Gacha pack distribution system |

### Backend Services

- **API Server** (`/api`): RESTful API with Echo framework
- **Indexer** (`/indexer`): Listens to blockchain events and syncs to database
- **Database**: PostgreSQL with Ent ORM

### Frontend Features

- **Authentication**: Magic Link email login + FCL wallet support
- **Event Management**: Create, browse, register, and check-in
- **Marketplace**: List and purchase NFTs
- **Profile**: Customize profile with featured moments
- **Gacha Shop**: Purchase and reveal accessory packs

## 🔗 API Documentation

Once the backend is running, visit:

```
http://localhost:8000/swagger/index.html
```

Key endpoints:
- `GET /events` - List all events
- `GET /events/:id` - Get event details
- `GET /moments` - Browse moments feed
- `GET /users/:address` - Get user profile
- `GET /marketplace/listings` - Browse marketplace
- `POST /upload` - Upload images to IPFS

## 🧪 Development

### Generate Swagger Docs

```bash
cd backend
swag init -g api/main.go
```

### Generate Ent Code

```bash
cd backend
go generate ./ent
```

### Build Frontend

```bash
cd frontend
bun run build
```

## 🌐 Deployment

### Backend

1. Set production environment variables
2. Build: `go build -o api ./api`
3. Run migrations (Ent auto-creates schema)
4. Deploy API and indexer as separate services

### Frontend

1. Build: `bun run build`
2. Deploy `dist/` folder to static hosting (Vercel, Netlify, etc.)
3. Set environment variables in hosting platform

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- Built on [Flow Blockchain](https://flow.com/)
- NFT Storefront V2 by Flow team
- Magic Link for authentication
- Ent framework for Go ORM

## 📧 Contact

- GitHub: [@harkon666](https://github.com/harkon666)
- Project Link: [https://github.com/harkon666/flow-landmark-nft](https://github.com/harkon666/flow-landmark-nft)

---

Made with ❤️ on Flow Blockchain
