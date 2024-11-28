# README: Firewall Packet Monitoring

## Overview

This project is a network monitoring tool that tracks and manages network traffic using Windows Firewall rules. It leverages the `scapy` library for packet sniffing, `streamlit` for a web interface, and `plotly` for visualizing the data. The application allows the user to monitor and control network packets by blocking and unblocking ports, as well as viewing detailed information on packet statuses. I wdid this project as my mini project with Soundarya R, Ilin Sugirtha Nixon

### Key Features:
- **Packet Sniffing:** Capture packets from a specified network interface and log details about them.
- **Firewall Management:** Block or unblock TCP ports via Windows Firewall directly from the app.
- **Real-Time Packet Status:** View live packet details and determine whether they are "Blocked" or "Allowed".
- **Data Visualization:** Display packet statistics in an interactive, stacked bar chart grouped by source IP and packet status.
- **Firewall IP Display:** Show the local firewall's IP address.

## Requirements
Before running the project, make sure you have the following Python packages installed:
- `scapy` - for packet sniffing and manipulation
- `streamlit` - for the web interface
- `pandas` - for data handling
- `plotly` - for creating interactive visualizations

You can install the required libraries by running:

```bash
pip install scapy streamlit pandas plotly
```

## Usage

### 1. **Run the Streamlit app:**

To start the Streamlit app, simply run the following command in your terminal:

```bash
streamlit run app.py
```

Replace `app.py` with the filename if you saved it with a different name.

### 2. **Block or Unblock Ports:**
- Select a port from the dropdown menu to block or unblock.
- Click the "Block Port" button to add the selected port to the blocked list.
- Click the "Allow Port" button to remove the selected port from the blocked list and allow it again.

### 3. **View Packet Information:**
- The app will display a table with packet details, including the source IP, destination IP, source port, destination port, protocol, and whether the packet was allowed or blocked.
- You can adjust the `packet_count` variable in the script to change how many packets are captured during sniffing.

### 4. **Visualize Packet Status:**
- The app will generate a stacked bar chart that shows the number of packets by source IP, broken down by whether they were allowed or blocked.

### 5. **View the Firewall IP Address:**
- The app will display the local firewall's IP address beneath the packet details table.

## Firewall Management

### **Block a Port:**
To block a port:
1. Select a port from the dropdown menu of allowed ports.
2. Press the "Block Port" button. The selected port will be added to the blocked ports list, and a corresponding firewall rule will be added to block incoming traffic on that port.

### **Unblock a Port:**
To unblock a port:
1. Select a port from the dropdown menu of blocked ports.
2. Press the "Allow Port" button. The selected port will be removed from the blocked ports list, and the firewall rule will be deleted to allow incoming traffic on that port again.

## Code Breakdown

### Packet Sniffing:
The script uses the `scapy` library's `sniff` function to capture packets on the specified network interface. The function processes each packet to determine whether it should be blocked based on its source/destination IP or port.

### Firewall Management:
To block or unblock ports, the script uses the Windows command-line tool `netsh` to modify firewall rules. These actions are performed by the `block_port_in_windows` and `unblock_port_in_windows` functions.

### Data Visualization:
The packet data is collected in a DataFrame and then grouped by source IP and packet status. A stacked bar chart is created using `plotly` to visualize the number of packets from each source IP that are allowed or blocked.

### Streamlit UI:
The app is powered by Streamlit to provide an easy-to-use interface. The user can interact with the dropdown menus, see live updates of packet data, and view the firewall's IP address and packet status visualizations.

## Example Output

### Packet Table
| Source IP        | Destination IP   | Source Port | Destination Port | Protocol | Status  |
|------------------|------------------|-------------|------------------|----------|---------|
| 192.168.1.50     | 192.168.1.100    | 12345       | 80               | TCP      | Blocked |
| 192.168.1.101    | 192.168.1.200    | 8080        | 8080             | TCP      | Allowed |

### Stacked Bar Chart
The stacked bar chart will display the number of packets from each source IP, with colors representing whether the packet was allowed or blocked.

## Contributing

Feel free to contribute to this project by opening issues or submitting pull requests. Improvements and enhancements are always welcome.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

Please use this tool responsibly. The modification of firewall rules and sniffing of network packets may violate local laws or organizational policies. Always ensure you have permission before using this tool on any network.
