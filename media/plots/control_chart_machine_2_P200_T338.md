
library(qcc)

# Filter data for Machine 2, Pressure = 200kPa, Temp = 338K
data_m2 <- subset(X011, Machine == 2 & Pressure == 200 & Temperature == 338)

# Ensure PartLength is a numeric vector
part_length_m2 <- as.numeric(data_m2$PartLength)

# Create a qcc object for Individuals chart
qcc_obj_m2_xbar <- qcc(part_length_m2, type="xbar.one", plot=FALSE)

# Save plot to PNG
png(filename = "/content/project/media/plots/control_chart_machine_2_P200_T338.png", width = 800, height = 600)
plot(qcc_obj_m2_xbar, chart.all=FALSE, title=paste0("Control Chart for Machine ", machine_id, " (P=", pressure_val, "kPa, T=", temperature_val, "K)"))
dev.off()
