# OGC API - Connected Systems: Live Server Testing

**PRIVATE REPOSITORY - Contains Server Credentials**

This repository contains live server integration tests and validation demos for the [ogc-client-CSAPI](https://github.com/sbolling/ogc-client-CSAPI) library implementation.

## 🔒 Security Notice

This repository is **PRIVATE** because it contains:
- Live server URLs
- Authentication credentials
- Deployment-specific details

**DO NOT** make this repository public or share credentials outside authorized personnel.

## 📋 Purpose

Validate the ogc-client-CSAPI library against a real OGC API - Connected Systems server:
- Integration test suite (16+ tests)
- Live demonstration scripts
- Performance benchmarks
- Real-world compatibility verification

## 🎯 Test Server

- **Implementation**: OpenSensorHub
- **API**: OGC API - Connected Systems (draft spec)
- **Authentication**: HTTP Basic Authentication
- **Data**: Real-time sensor data (drones, mobile devices, environmental sensors)
- **Resources**: Systems, Datastreams, Observations, Deployments, Procedures, Sampling Features

## 🚀 Quick Start

### Prerequisites

```bash
# Ensure main library is available
ls ../ogc-client-CSAPI  # Should exist
```

### Installation

```bash
# Install dependencies (includes link to main library)
npm install

# Copy environment template
cp .env.example .env

# Edit .env with actual credentials (DO NOT COMMIT)
notepad .env
```

### Running Tests

```bash
# Run integration test suite
npm test

# Run specific demo
npm run demo:connection
npm run demo:navigator
npm run demo:library

# Run all demos
npm run demo:all
```

## 📁 Repository Structure

```
ogc-client-csapi-live-tests/
├── README.md                           # This file
├── .env.example                        # Template for credentials
├── .env                                # Actual credentials (gitignored)
├── .gitignore                          # Protect sensitive files
├── package.json                        # Dependencies and scripts
├── tsconfig.json                       # TypeScript configuration
├── tests/
│   ├── live-server.integration.spec.ts # Full integration test suite
│   └── setup.ts                        # Test configuration
├── demos/
│   ├── csapi-live-connection.js        # Step-by-step server exploration
│   ├── csapi-navigator-demo.js         # Navigator URL builder pattern
│   └── csapi-library-demo.js           # Using built library directly
├── docs/
│   ├── server-findings.md              # Detailed server analysis
│   ├── test-results.md                 # Latest test execution logs
│   └── validation-report.md            # Comprehensive validation report
└── scripts/
    └── run-all-tests.sh                # Convenience script for all tests
```

## 🔧 Configuration

### Environment Variables

Create `.env` file with:

```bash
CSAPI_LIVE_SERVER=http://your-server-url/api
CSAPI_LIVE_USER=your-username
CSAPI_LIVE_PASS=your-password
```

### Linking to Main Library

The `package.json` references the main library as a local dependency:

```json
{
  "dependencies": {
    "@camptocamp/ogc-client": "file:../ogc-client-CSAPI"
  }
}
```

After changes to the main library, run:
```bash
npm install  # Refreshes the link
```

## 📊 Test Coverage

### Integration Tests (16 tests)
- ✅ Server discovery and conformance
- ✅ Systems collection and individual retrieval
- ✅ Datastreams listing and filtering
- ✅ Observations with temporal queries
- ✅ Sub-resource navigation (system → datastreams)
- ✅ Query parameters (limit, q, bbox, datetime)
- ✅ Error handling (404, 401)
- ✅ Link following and pagination
- ✅ Format detection
- ✅ Type validation

### Demonstration Scripts (3 scripts)
- ✅ Direct connection pattern with manual fetch
- ✅ Navigator URL builder pattern validation
- ✅ Library integration with authentication

## 📈 Validation Results

Latest test run: *Run `npm test` to update*

- **Systems Found**: 5 (drone, mobile devices)
- **Datastreams Found**: 3 (GPS, temperature, status)
- **Observations**: Real-time streaming validated
- **Response Time**: Sub-second for all endpoints
- **Authentication**: Basic Auth working correctly
- **Format Compatibility**: Handles multiple collection formats

## 🔄 CI/CD

GitHub Actions workflow runs tests:
- **Schedule**: Daily at noon UTC
- **Trigger**: Manual via workflow_dispatch
- **Secrets**: CSAPI_LIVE_SERVER, CSAPI_LIVE_USER, CSAPI_LIVE_PASS

View workflow runs in Actions tab.

## 📝 Adding New Tests

1. Add test to `tests/live-server.integration.spec.ts`
2. Run locally: `npm test`
3. Document findings in `docs/test-results.md`
4. Commit and push (credentials are gitignored)

## 🤝 Sharing Results

### Public Information (Safe to Share)
- ✅ Test results (pass/fail counts)
- ✅ Performance metrics
- ✅ Server capabilities discovered
- ✅ Compatibility notes

### Private Information (Keep Secret)
- ❌ Server URL
- ❌ Credentials
- ❌ Deployment details
- ❌ System IDs if sensitive

## 📚 Documentation

- **[Server Findings](docs/server-findings.md)**: Detailed analysis of server behavior
- **[Test Results](docs/test-results.md)**: Execution logs and metrics
- **[Validation Report](docs/validation-report.md)**: Comprehensive validation evidence

## 🔗 Related Repositories

- **Main Library**: [ogc-client-CSAPI](https://github.com/sbolling/ogc-client-CSAPI) (public)
- **Upstream**: [camptocamp/ogc-client](https://github.com/camptocamp/ogc-client) (target for contribution)

## 📧 Support

For issues or questions about live server testing, contact the repository maintainer.

---

**Remember**: This repository is private for a reason. Protect the credentials! 🔐
