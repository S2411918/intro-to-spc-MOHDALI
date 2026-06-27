
library(qcc)

# Filter data for Machine 2, Pressure = 200kPa, Temp = 338K
data_m2 <- subset(X011, Machine == 2 & Pressure == 200 & Temperature == 338)

LSL = 45
USL = 55
TARGET = 50

# Create a qcc object for capability analysis
qcc_obj_m2_cap <- qcc(as.numeric(data_m2$PartLength), type="xbar.one", plot=FALSE)

# Process Capability Analysis
pc_m2 <- process.capability(qcc_obj_m2_cap, spec.limits=c(LSL, USL), target=TARGET)

# Save plot to PNG
png(filename = "/content/project/media/plots/process_capability_machine_2_P200_T338.png", width = 800, height = 600)
plot(pc_m2, title=paste0("Process Capability for Machine ", machine_id, " (P=", pressure_val, "kPa, T=", temperature_val, "K)"))
dev.off()
