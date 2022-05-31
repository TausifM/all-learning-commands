In the project AJAX is used for the api calling which is in the Account Services


# BELOW THE CODE in Account Services File

Below Code for Ajax GET API
  public getEstimateDetails(estimateDetailsHandler: RespHandler): void {
    this.get({
      url: "/estimate_details_v1",
      errorHook: estimateDetailsHandler.error,
    }).then(estimateDetailsHandler.success);
  }


And Calling this get API in the another File

    const getEstimateDetails = () => {
        const estimate = AccountService.o.getEstimateDetails(estimateDetailsHandler);
        console.log(estimate);
      }
      const estimateDetailsHandler: RespHandler = {
        success: estimateDetailsFunction,
      };
      function estimateDetailsFunction (estimate){
        console.log(estimate.data.data);
        if (estimate.data.data._id) {
          const invoiceData = {
            invoiceData: estimate.data.data.boardItem,
            isInvoice: estimate.data.data.isInvoice,
            locationDetails: estimate.data.data.locationDetail,
            locationFullData: estimate.data.data.locationFullData,
            locationDetail: estimate.data.data.boardItem.l_id,
            onPayment: onPaymentfn,
          };
          console.log(invoiceData);
          setAppData({
            ...appData,
            invoiceData: invoiceData,
          });
        }
      }