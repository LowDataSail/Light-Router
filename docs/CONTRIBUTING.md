# Contributing to Light Router

*How to contribute to the Light Router project*

---

## **🎉 Welcome!**

We're excited that you're interested in contributing to **Light Router**! This document provides guidelines for contributing to the project.

---

## **📋 Code of Conduct**

By participating in this project, you agree to abide by the [Code of Conduct](CODE_OF_CONDUCT.md). Please read it before contributing.

---

## **🤔 How Can I Contribute?**

### **Reporting Bugs**

If you find a bug, please:

1. **Check existing issues** to see if it's already been reported
2. **Create a new issue** with:
   - A clear, descriptive title
   - Steps to reproduce the bug
   - Expected vs. actual behavior
   - Screenshots or error messages (if applicable)
   - Your environment (OS, Python version, etc.)
   - Any relevant logs or data

### **Suggesting Features**

If you have an idea for a new feature:

1. **Check existing issues** to see if it's already been suggested
2. **Create a new issue** with:
   - A clear description of the feature
   - The problem it solves
   - Any relevant use cases
   - Mockups or examples (if applicable)

### **Contributing Code**

We welcome pull requests! Please:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/your-feature`)
3. **Commit your changes** with clear, descriptive messages
4. **Push to your fork**
5. **Open a pull request** to the main repository

### **Improving Documentation**

Documentation is just as important as code! You can help by:

- Fixing typos or errors
- Adding missing information
- Improving clarity or organization
- Adding examples or tutorials

---

## **🚀 Getting Started**

### **Prerequisites**

- Python 3.10+
- Git
- pip

### **Setting Up**

```bash
# Fork the repository
git clone https://github.com/LowDataSail/Light-Router.git
cd Light-Router

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install in development mode
pip install -e .

# Install pre-commit hooks
pre-commit install
```

### **Running Tests**

```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_module.py

# Run with coverage
pytest --cov=src
```

### **Building Documentation**

```bash
# Install mkdocs
pip install mkdocs mkdocs-material

# Serve documentation locally
mkdocs serve

# Build documentation
mkdocs build
```

---

## **📝 Pull Request Guidelines**

### **Before Submitting**

1. **Run tests** to ensure nothing is broken
2. **Run linting** to check code style:
   ```bash
   flake8 src/
   black --check src/
   ```
3. **Update documentation** if your changes affect the API or usage
4. **Add tests** for new functionality
5. **Update CHANGELOG.md** if your changes are user-facing

### **Pull Request Requirements**

1. **Clear title** describing the change
2. **Detailed description** explaining:
   - What the change does
   - Why it's needed
   - Any relevant context or issues
3. **Linked to an issue** (if applicable)
4. **Passing tests** and linting
5. **Code review** from at least one maintainer

### **Commit Messages**

Please follow these guidelines for commit messages:

- Use the **present tense** ("Add feature" not "Added feature")
- Use the **imperative mood** ("Move cursor to..." not "Moves cursor to...")
- **Limit the first line to 72 characters** or less
- **Reference issues** when applicable (e.g., "Fix #123")
- **Separate subject from body** with a blank line
- **Wrap the body** at 72 characters

**Good example:**
```
Add delta encoding for weather data

Implement delta encoding to reduce data usage by 70-90%.
This addresses the primary goal of low data routing.

Fix #42
```

**Bad example:**
```
fixed bug
```

---

## **🎨 Code Style**

### **Python**

- Follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guide
- Use **4 spaces** for indentation
- **Black** is used for code formatting:
  ```bash
  black src/
  ```
- **Flake8** is used for linting:
  ```bash
  flake8 src/
  ```
- **Docstrings** should follow [Google style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings)

### **Imports**

- Group imports in the following order:
  1. Standard library imports
  2. Third-party imports
  3. Local application imports
- Separate groups with a blank line
- Sort imports alphabetically within each group

**Example:**
```python
import os
import sys
from typing import List, Optional

import numpy as np
import pandas as pd

from src.data_pipeline import grib_parser
from src.utils import helpers
```

### **Naming**

- **Variables:** `snake_case`
- **Functions:** `snake_case`
- **Classes:** `PascalCase`
- **Constants:** `UPPER_SNAKE_CASE`
- **Private members:** `_leading_underscore`
- **Protected members:** `_leading_underscore` (Python convention)

### **Type Hints**

- Use type hints for all function signatures
- Use type hints for variables when it improves clarity
- Use `Optional` for parameters that can be `None`
- Use `Union` for parameters that can be multiple types

**Example:**
```python
def calculate_route(
    start: Tuple[float, float],
    end: Tuple[float, float],
    weather_data: Optional[Dict] = None,
) -> List[Tuple[float, float]]:
    ...
```

---

## **📁 Project Structure**

```
Light-Router/
├── docs/                      # Documentation
│   ├── index.md              # Home page
│   ├── PROJECT_DESCRIPTION.md # Full project overview
│   ├── literature-review.md   # Literature review
│   ├── benchmarking.md        # Benchmarking methodology
│   ├── market-positioning.md  # Market positioning
│   ├── objectives.md         # Core objectives
│   ├── setup.md              # Setup guide
│   ├── architecture.md        # Architecture documentation
│   ├── CONTRIBUTING.md       # This file
│   └── CODE_OF_CONDUCT.md     # Code of conduct
├── src/                       # Source code
│   ├── __init__.py
│   ├── data_pipeline/        # Data ingestion and optimization
│   │   ├── __init__.py
│   │   ├── grib_parser.py     # GRIB file parser
│   │   ├── delta_encoder.py   # Delta encoding
│   │   ├── region_filter.py   # Region filtering
│   │   ├── cache_manager.py  # Predictive caching
│   │   └── weather_client.py # Weather data client
│   ├── routing_engine/       # Core routing algorithms
│   │   ├── __init__.py
│   │   ├── isochrone.py       # Isochrone routing
│   │   ├── hierarchical_astar.py # Hierarchical A*
│   │   ├── incremental.py     # Incremental updates
│   │   └── constraints.py     # Safety constraints
│   ├── ai_models/            # AI/ML models
│   │   ├── __init__.py
│   │   ├── forecast_error.py  # Forecast error modeling
│   │   ├── event_detection.py # Extreme event detection
│   │   └── route_optimizer.py # Route optimization
│   └── utils/                # Utility functions
│       ├── __init__.py
│       ├── weather_utils.py  # Weather utilities
│       ├── boat_utils.py     # Boat performance utilities
│       └── visualization.py   # Visualization utilities
├── tests/                     # Tests
│   ├── __init__.py
│   ├── test_data_pipeline.py # Data pipeline tests
│   ├── test_routing.py        # Routing engine tests
│   └── test_ai_models.py      # AI model tests
├── benchmarks/                # Benchmarking scripts
│   ├── __init__.py
│   ├── head_to_head.py        # Head-to-head comparison
│   ├── historical_replay.py   # Historical route replay
│   └── synthetic_scenarios.py # Synthetic scenario tests
├── configs/                   # Configuration files
│   ├── boat_polars.yaml       # Boat performance curves
│   ├── infoclimat_config.yaml # Infoclimat API settings
│   └── routing_settings.yaml # Routing parameters
├── scripts/                   # Helper scripts
│   ├── setup_environment.sh   # Environment setup
│   ├── run_benchmarks.sh      # Benchmark runner
│   └── deploy_edge.sh         # Edge deployment
├── mkdocs.yml                 # Documentation configuration
├── requirements.txt           # Python dependencies
├── pyproject.toml             # Project metadata
├── LICENSE                    # MIT License
└── README.md                  # Project overview
```

---

## **🔧 Development Workflow**

### **1. Fork the Repository**

```bash
git clone https://github.com/LowDataSail/Light-Router.git
cd Light-Router
git remote add upstream https://github.com/LowDataSail/Light-Router.git
```

### **2. Create a Feature Branch**

```bash
git checkout -b feature/your-feature
git push origin feature/your-feature
```

### **3. Make Your Changes**

- Make your changes in the feature branch
- Commit your changes with clear messages
- Push to your fork

### **4. Open a Pull Request**

- Go to the [Light Router repository](https://github.com/LowDataSail/Light-Router)
- Click "New pull request"
- Select your feature branch
- Fill in the pull request template
- Submit for review

### **5. Address Feedback**

- Respond to review comments
- Make requested changes
- Push updates to your branch
- Request re-review when ready

### **6. Merge**

Once approved, a maintainer will merge your pull request.

---

## **📊 Testing**

### **Unit Tests**

- Use `pytest` for unit tests
- Place tests in the `tests/` directory
- Name test files `test_*.py`
- Use descriptive test function names

**Example:**
```python
def test_delta_encoding():
    """Test that delta encoding reduces data size by 70-90%."""
    original_data = load_grib_file("test.grib2")
    encoded_data = delta_encode(original_data)
    
    assert len(encoded_data) < len(original_data) * 0.3

def test_route_calculation():
    """Test that route calculation produces valid waypoints."""
    router = IsochroneRouter()
    route = router.calculate_route((0, 0), (10, 10))
    
    assert len(route) > 0
    assert route[0] == (0, 0)
    assert route[-1] == (10, 10)
```

### **Integration Tests**

- Test interactions between components
- Place in `tests/integration/`
- Use temporary directories for test files

### **Benchmark Tests**

- Test performance and scalability
- Place in `benchmarks/`
- Use `pytest-benchmark` for performance testing

---

## **📖 Documentation**

### **Writing Documentation**

- Use **Markdown** for documentation
- Follow the existing style and structure
- Use **clear, concise language**
- Include **examples** where helpful
- Link to **relevant resources**

### **Documentation Standards**

- **Headings:** Use ATX-style headings (`#`, `##`, etc.)
- **Lists:** Use hyphens for unordered lists, numbers for ordered lists
- **Code:** Use fenced code blocks with language specification
- **Links:** Use descriptive link text
- **Images:** Place in `docs/assets/images/` and reference with relative paths

---

## **🎁 Recognition**

All contributions are **valued and appreciated**! Contributors will be recognized in:

- The [CONTRIBUTORS.md](CONTRIBUTORS.md) file
- Release notes
- GitHub contribution graph
- Project documentation

---

## **📄 License**

By contributing to Light Router, you agree that your contributions will be licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---

## **🙏 Thank You!**

Thank you for contributing to Light Router! Your contributions help make this project better for everyone.

---

**© 2026 LowDataSail**
**Last Updated:** September 6, 2026
**Version:** 1.0
