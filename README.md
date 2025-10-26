# IVT-Analysis
Problem Statement : We need to determine why some apps were marked IVT (Invalid Traffic) and others were not, using the provided metrics and their patterns over time.

Focus Area On : The following columns are most diagnostic for IVT (suspicious/fake traffic):
requests_per_idfa – abnormally high ⇒ possible automation/bot activity.


impressions_per_idfa – abnormally low ⇒ requests without genuine ads shown.


idfa_ip_ratio – high ⇒ multiple fake “devices” from the same IP (proxy/data center).


idfa_ua_ratio – high ⇒ many devices sharing same User-Agent (spoofing).


unique_ips vs unique_idfas trend – low IP diversity often means non-human traffic.
Analysis : 
Apps not Marked IVT : Typical observed behavior:
idfa_ip_ratio ≈ 1 → one device per IP (normal for consumer networks).


idfa_ua_ratio ≤ 2–3 → variety of User-Agents → diverse real devices.


requests_per_idfa moderate (e.g., <1000) → normal user ad consumption rate.


impressions_per_idfa proportional → real requests leading to impressions.


Stable trends over time → no sudden spikes or overnight volume surges.
Interpretation : Traffic looks organic — multiple unique devices, distributed IPs, consistent UA mix, stable activity. These indicate real users generating ad requests.

Apps Marked IVT Early : Likely characteristics:
Sudden spike in total_requests without corresponding rise in unique_idfas.


requests_per_idfa and idfa_ip_ratio jump sharply.


unique_uas drop → fewer User-Agents serving many devices.


impressions_per_idfa falls → ad requests not turning into impressions.


idfa_ua_ratio >10 or even >50 → hundreds of “devices” pretending to use same UA.
Interpretation : The system detected device spoofing or proxy-based traffic early — many “devices” from same IP or UA. Hence, the app flagged IVT quickly.
Apps Marked IVT Later : Likely pattern:
Initially behaved normally (metrics similar to non-IVT apps).


Gradually requests_per_idfa and idfa_ip_ratio increased.


Traffic started showing clusters of same IPs or UAs.


Small but growing mismatch between requests vs impressions.


Eventually IVT threshold crossed after sustained anomalies.
Interpretation : Traffic quality degraded over time — possibly due to introduction of traffic buying, SDK fraud, or traffic manipulation by third-party ad sources.
The system needed historical data to confirm persistent anomaly before marking IVT.
Conclusion : The IVT classification correlates strongly with increasing idfa_ip_ratio, idfa_ua_ratio, and requests_per_idfa.
Apps flagged early show clear fraud signals right from the start.
Apps flagged later show gradual traffic degradation — likely due to new traffic sources or behavior shifts.
Apps never flagged maintain stable, realistic metrics across all dimensions.
