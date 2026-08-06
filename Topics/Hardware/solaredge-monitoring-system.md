# SolarEdge Monitoring System
Added: 2026-08-06
Status: [Active]
Tags: [solar, energy-monitoring, photovoltaic, home-automation, alerting]

## Summary
System for monitoring SolarEdge photovoltaic installations using credentials-based access to the SolarEdge monitoring portal. Designed to detect anomalies in power consumption patterns, particularly for hot water circuit operation (~3kW draw between 10am-2pm), to provide early warning of electrical issues before they require emergency service calls.

## Key Points
- Uses Playwright for automated login and data extraction from SolarEdge monitoring website
- GitHub Actions for scheduled data collection and analysis
- GitHub Pages for visualization of solar production and consumption data
- Alerting mechanism for missing expected power draw patterns
- Focus on hot water circuit monitoring (~3kW draw 10am-2pm) as early failure indicator
- Designed to avoid weekend call-out fees by detecting issues during weekdays

## Resources
- [SolarEdge Monitoring Portal](https://monitoring.solaredge.com) - Main monitoring interface
- [Playwright Documentation](https://playwright.dev) - Browser automation framework
- [GitHub Actions Documentation](https://docs.github.com/en/actions) - CI/CD for scheduled tasks
- [GitHub Pages Documentation](https://docs.github.com/en/pages) - Free hosting for visualization

## Related Topics
- [[pulse-pve-monitoring]] - Similar Proxmox monitoring approach
- [[proxmox-ve-homelab]] - Homelab infrastructure context

## Implementation Plan
1. Create GitHub repository for SolarEdge monitoring code
2. Develop Playwright script to login to SolarEdge portal and extract:
   - Real-time power production/consumption
   - Historical data for pattern analysis
   - Hot water circuit power draw (if available via granular monitoring)
3. Set up GitHub Actions workflow to:
   - Run monitoring script on schedule (every 15-30 minutes during daylight hours)
   - Store collected data in repository
   - Generate alert if expected hot water draw pattern is missing
4. Create GitHub Pages site to display:
   - Real-time solar production/consumption gauges
   - Historical graphs showing daily patterns
   - Alert status for hot water circuit operation
5. Implement anomaly detection for:
   - Missing ~3kW draw between 10am-2pm on expected days
   - Sudden drops in solar production
   - Unusual consumption patterns

## Technical Considerations
- Authentication: Handle SolarEdge login securely using GitHub Secrets
- Data storage: Use JSON files or CSV in repository for historical data
- Visualization: Consider Chart.js, Plotly, or similar for graphs
- Alerting: GitHub Actions can create Issues or send notifications via webhook
- Rate limiting: Respect SolarEdge website terms of service
- Error handling: Graceful degradation when website changes or login fails