# 🚨 Project G - Advanced Gas Monitoring System

A comprehensive real-time gas leak detection and monitoring system using MQ-5 sensors, featuring dual detection systems for both home safety and outdoor industrial monitoring.

## 🌟 Features

### 🔥 **Dual Detection Systems**
- **🏠 Home Safety System**: Conservative thresholds (2000/4000 ppm) for immediate safety alerts
- **🌍 Outdoor Monitor System**: Advanced signal processing with configurable thresholds for LPG/Methane

### 📊 **Real-Time Monitoring**
- Live sensor data visualization with interactive charts
- Multiple dashboard views (Basic, Modern, Advanced)
- Real-time anomaly detection and alerting
- Historical data analysis and CSV export

### 🛡️ **Advanced Anomaly Detection**
- **Enhanced Anomaly Detector**: Multi-method detection (Statistical + Absolute + Trend + Velocity + Home Safety)
- **Outdoor Gas Monitor**: Signal processing with moving averages, hysteresis, and voting logic
- Rate-of-rise detection for rapid gas concentration changes
- Configurable thresholds and parameters

### 🎨 **Modern UI/UX**
- Responsive web interface with Tailwind CSS
- Interactive charts using Chart.js
- Real-time data updates
- Mobile-friendly design

## 🏗️ System Architecture

```
MQ-5 Sensor → Flask Backend → Dual Detection Systems
    ↓              ↓                    ↓
Raw Data    →  Data Processing  →  Enhanced Anomaly Detector
    ↓              ↓                    ↓
Web UI      ←  API Endpoints    ←  Outdoor Gas Monitor
```

## 📋 Prerequisites

- Python 3.8+
- Flask
- Pandas
- NumPy
- Scikit-learn
- Joblib

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/hemanthsunkara05/Project-G.git
   cd Project-G
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**
   ```bash
   python app.py
   ```

5. **Access the dashboards**
   - Basic Dashboard: `http://127.0.0.1:5000/dashboard`
   - Modern Dashboard: `http://127.0.0.1:5000/modern`
   - Advanced Dashboard: `http://127.0.0.1:5000/advanced`

## 📊 Dashboard Overview

### 🏠 **Basic Dashboard** (`/dashboard`)
- Simple MQ-5 sensor monitoring
- Real-time chart visualization
- Basic anomaly detection
- CSV data export

### 🎨 **Modern Dashboard** (`/modern`)
- Enhanced UI with Tailwind CSS
- Advanced charting capabilities
- Real-time sensor status cards
- Comprehensive anomaly information

### 🌟 **Advanced Dashboard** (`/advanced`)
- **Dual System Comparison**: Side-by-side display of both detection systems
- **System Overview**: Status, thresholds, and detection methods
- **Real-time Charts**: Comparison of both systems
- **Detailed Data Table**: Comprehensive monitoring information

## 🔧 Configuration

### Home Safety Thresholds
Configured in `enhanced_anomaly_detector.py`:
```python
'home_safety_low': 2000,    # ppm - Early warning
'home_safety_high': 4000    # ppm - Danger level
```

### Outdoor Monitor Configuration
Configured in `gas_monitor_config.json`:
```json
{
  "gas_types": {
    "methane": {
      "low_threshold": 2500,
      "high_threshold": 7500
    },
    "lpg": {
      "low_threshold": 1000,
      "high_threshold": 3000
    }
  }
}
```

## 📡 API Endpoints

### Data Input
- `POST /data` - Send MQ-5 sensor data (triggers both systems)
- `POST /outdoor-gas-data` - Send outdoor gas monitoring data

### Data Retrieval
- `GET /dashboard-data` - Get sensor data for basic dashboard
- `GET /api/sensors` - Get sensor data for modern dashboard
- `GET /outdoor-gas-status` - Get outdoor monitor status

### Testing
- `GET /test-enhanced-detection` - Test enhanced anomaly detector
- `GET /test-outdoor-monitor` - Test outdoor gas monitor
- `GET /add-sample-data` - Add sample sensor data

## 🔍 Detection Methods

### Enhanced Anomaly Detector
1. **Statistical Detection**: Based on historical data patterns
2. **Absolute Thresholds**: Fixed warning/critical levels
3. **Trend Analysis**: Detects gradual increases over time
4. **Velocity Detection**: Rate-of-change analysis
5. **Home Safety**: Conservative thresholds for immediate alerts

### Outdoor Gas Monitor
1. **Signal Processing**: Moving average and rolling median
2. **Rate-of-Rise Detection**: Rapid increase detection
3. **Hysteresis**: Prevents alert flickering
4. **Voting Logic**: Requires multiple indicators for confirmation
5. **Configurable Thresholds**: Different levels for LPG/Methane

## 📈 Alert Levels

### Home Safety System
- **Normal**: < 2000 ppm
- **Early Warning**: 2000-3999 ppm
- **Danger - Evacuate**: ≥ 4000 ppm

### Outdoor Monitor System
- **Normal**: Below low threshold
- **Early Warning**: Between low and high thresholds
- **Danger**: Above high threshold

## 🗂️ File Structure

```
Project-G/
├── app.py                          # Main Flask application
├── enhanced_anomaly_detector.py    # Home safety detection system
├── outdoor_gas_monitor.py          # Outdoor monitoring system
├── gas_monitor_config.json         # Outdoor system configuration
├── train_model.py                  # Model training script
├── templates/
│   ├── index.html                  # Basic dashboard
│   ├── modern_dashboard.html       # Modern UI dashboard
│   ├── advanced_dashboard.html     # Dual system dashboard
│   └── react_dashboard.html        # React frontend placeholder
├── static/
│   └── style.css                   # Basic dashboard styles
├── model/
│   ├── isolation_forest_model.pkl  # Trained ML model
│   └── scaler.pkl                  # Data scaler
├── data/
│   └── sensor_data.csv             # Historical sensor data
└── requirements.txt                # Python dependencies
```

## 🧪 Testing

### Test Enhanced Detection
```bash
curl http://127.0.0.1:5000/test-enhanced-detection
```

### Test Outdoor Monitor
```bash
curl http://127.0.0.1:5000/test-outdoor-monitor
```

### Send Test Data
```bash
curl -X POST http://127.0.0.1:5000/data \
  -H "Content-Type: application/json" \
  -d '{"value": 3000}'
```

## 🔧 Customization

### Modify Thresholds
1. **Home Safety**: Edit `enhanced_anomaly_detector.py`
2. **Outdoor Monitor**: Edit `gas_monitor_config.json`

### Add New Gas Types
1. Add configuration to `gas_monitor_config.json`
2. Update detection logic in `outdoor_gas_monitor.py`

### Customize UI
1. Modify HTML templates in `templates/`
2. Update CSS styles in `static/style.css`

## 🚨 Safety Features

- **Immediate Alerts**: Home safety system provides instant notifications
- **Redundant Detection**: Dual systems ensure comprehensive monitoring
- **Configurable Thresholds**: Adjustable for different environments
- **Historical Analysis**: Data logging for trend analysis
- **Export Capabilities**: CSV download for external analysis

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions:
- Create an issue on GitHub
- Contact the development team
- Check the documentation

## 🔮 Future Enhancements

- [ ] Email/SMS alert integration
- [ ] Mobile app development
- [ ] Cloud data storage
- [ ] Machine learning model improvements
- [ ] Additional sensor support
- [ ] Advanced analytics dashboard

---

**⚠️ Safety Notice**: This system is designed for monitoring and early warning. Always follow proper safety procedures and evacuate immediately if gas leaks are detected.