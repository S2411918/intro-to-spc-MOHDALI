
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter data for Machine 3, Pressure = 200kPa, Temp = 338K
data_m3 <- subset(X011, Machine == 3 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m3_cap <- qcc(data_m3$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m3 <- process.capability(qcc_obj_m3_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Plot the process capability chart
pc_m3_plot <- plot(pc_m3, title=paste0("Process Capability for Machine 3 (P=200kPa, T=338K)"))

# Placeholder for saving R code
