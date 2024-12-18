package com.devsuperior.dsmeta.repositories;

import java.awt.print.Pageable;
import java.time.LocalDate;
import java.util.List;

import org.springframework.data.domain.Page;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;

import com.devsuperior.dsmeta.dto.SaleReportDTO;
import com.devsuperior.dsmeta.dto.SaleSummaryDTO;
import com.devsuperior.dsmeta.entities.Sale;

@Repository
public interface SaleRepository extends JpaRepository<Sale, Long> {

    @Query("SELECT new com.example.dto.SaleReportDTO(s.id, s.date, s.amount, s.seller.name) " +
           "FROM Sale s " +
           "WHERE (:minDate IS NULL OR s.date >= :minDate) " +
           "AND (:maxDate IS NULL OR s.date <= :maxDate) " +
           "AND (:name IS NULL OR LOWER(s.seller.name) LIKE LOWER(CONCAT('%', :name, '%')))")
    Page<SaleReportDTO> findSalesReport(LocalDate minDate, LocalDate maxDate, String name, Pageable pageable);

    @Query("SELECT new com.example.dto.SaleSummaryDTO(s.seller.name, SUM(s.amount)) " +
           "FROM Sale s " +
           "WHERE (:minDate IS NULL OR s.date >= :minDate) " +
           "AND (:maxDate IS NULL OR s.date <= :maxDate) " +
           "GROUP BY s.seller.name")
    List<SaleSummaryDTO> findSalesSummary(LocalDate minDate, LocalDate maxDate);
}

