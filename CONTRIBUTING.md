# Contributing to CESM Terrain and Snow Analysis

Thank you for your interest in contributing! This document provides guidelines for contributing to this project.

## How to Contribute

### Reporting Issues

If you find a bug or have a suggestion for improvement:

1. Check if the issue already exists in the [Issues](https://github.com/Austfi/CESM_terrain_snow/issues) section
2. Create a new issue with:
   - A clear, descriptive title
   - Detailed description of the problem or suggestion
   - Steps to reproduce (for bugs)
   - Expected vs. actual behavior
   - Any relevant error messages or screenshots

### Contributing Code

1. **Fork the repository**
   ```bash
   git clone https://github.com/Austfi/CESM_terrain_snow.git
   cd CESM_terrain_snow
   ```

2. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow existing code style
   - Add comments for complex logic
   - Update documentation as needed
   - Ensure notebooks run from top to bottom

4. **Test your changes**
   - Run all notebook cells
   - Verify outputs are correct
   - Check for any errors or warnings

5. **Commit your changes**
   ```bash
   git add .
   git commit -m "Description of your changes"
   ```

6. **Push and create a Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then create a Pull Request on GitHub with a clear description of your changes.

## Code Style Guidelines

### Python Code
- Follow PEP 8 style guidelines
- Use descriptive variable names
- Add docstrings for functions
- Keep functions focused and modular

### Jupyter Notebooks
- Clear markdown headers and documentation
- Well-commented code cells
- Organized cell structure
- Remove unnecessary output before committing

### Documentation
- Update README.md if adding new features
- Include docstrings for functions
- Add comments explaining complex calculations

## Areas for Contribution

We welcome contributions in these areas:

- **Additional locations**: Add more cities or mountain passes to analyze
- **Visualization improvements**: Enhance plots or add new visualizations
- **Statistical analysis**: Add new error metrics or comparison methods
- **Documentation**: Improve clarity, add examples, or fix typos
- **Code optimization**: Improve performance or code organization
- **Bug fixes**: Fix any issues you encounter

## Questions?

If you have questions about contributing, please open an issue with the `question` label.

Thank you for contributing to CESM Terrain and Snow Analysis! 🎉

