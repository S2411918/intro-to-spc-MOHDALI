
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter data for Machine 3, Pressure = 200kPa, Temp = 338K
data_m3 <- subset(X011, Machine == 3 & Pressure == 200 & Temperature == 338)

# Create a qcc object for Xbar chart
qcc_obj_m3_xbar <- qcc(data_m3$PartLength, type="xbar", plot=FALSE)

# Plot the control chart
cc_m3_plot <- plot(qcc_obj_m3_xbar, chart.all=FALSE, title=paste0("Control Chart for Machine 3 (P=200kPa, T=338K)"))

# Placeholder for saving R code
