
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter data for Machine 2, Pressure = 200kPa, Temp = 338K
data_m2 <- subset(X011, Machine == 2 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m2_cap <- qcc(data_m2$PartLength, type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m2 <- process.capability(qcc_obj_m2_cap, spec.limits=c(LSL, USL), target=TARGET, plot=FALSE)

# Plot the process capability chart
pc_m2_plot <- plot(pc_m2, title=paste0("Process Capability for Machine 2 (P=200kPa, T=338K)"))

# Placeholder for saving R code
